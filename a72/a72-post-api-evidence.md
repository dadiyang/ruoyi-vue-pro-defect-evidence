# A72 修后证据（2026-10-07 09:35:36，TCMS 引擎实例 43315 / job 2143 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（监听器对空 businessKey 跳过回写）。

同一流程（通用发起无 businessKey 的 oa_leave 实例）取消：

```
POST /admin-api/bpm/process-instance/create（无 businessKey）
→ {"code": 0, "data": "64ef12ca-c1ef-11f1-b29e-fee45c6e4f05"}

DELETE /admin-api/bpm/process-instance/cancel-by-admin
{"id": "64ef12ca-c1ef-11f1-b29e-fee45c6e4f05", "reason": "BPM-03 A72 无businessKey取消"}
→ {"code": 0, "data": true}
```

实例状态读回：status=4（已取消）。

对照与连带：
- 经业务单发起的请假（有 businessKey）取消仍同步回写请假单状态=4（同轮既有断言通过）；
- 修前腿遗留的卡死实例（无 businessKey、运行中）在修复部署后被正常取消，
  DB 核对 ACT_RU_EXECUTION 无 businessKey 的 oa_leave 运行实例残留 = 0。
