# A96 修后证据（2026-10-07 10:16:51，TCMS 引擎实例 43337 / job 2163 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（新错误码 1_009_003_004＋抛在位处）。

同一请求（非法状态值）：

```
PUT /admin-api/bpm/model/update-state
{"id": "26add2c8-c1f5-11f1-bb92-fee45c6e4f05", "state": 3}
→ {"code": 1009003004, "msg": "修改流程定义状态失败，状态值(3) 非法", "data": null}
```

受控拒绝后 GET /bpm/process-definition/list?suspensionState=1 该定义仍在激活面（状态未被改动）。

既有断言全部照旧通过：挂起(2)后定义在挂起面 suspensionState=2、挂起态发起受控拒绝 1009003003、
非模型管理员改状态受控拒绝 1009002007 且定义仍挂起、激活(1)后恢复可见并可发起、收尾清理等。
