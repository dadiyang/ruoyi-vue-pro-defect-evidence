# A96 修前证据（2026-10-07 10:15:27，TCMS 引擎实例 43336 / job 2162 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：本轮自建 SIMPLE 模型并部署→update-state state=2 挂起→state=1 激活（定义在激活面）。

请求（非法状态值）：

```
PUT /admin-api/bpm/model/update-state
{"id": "f50e939d-c1f4-11f1-827e-fee45c6e4f05", "state": 3}
→ {"code": 0, "msg": "", "data": true}     ← 返回成功
```

返回成功但服务端什么都没做：`updateProcessDefinitionState` 对未知值只记一条 ERROR 日志
（修改未知状态(3)）后静默返回（void），控制器照常包成 code=0 data=true，定义状态不变。
用例断言「应受控拒绝 1009003004」失败（判 FAIL）。
