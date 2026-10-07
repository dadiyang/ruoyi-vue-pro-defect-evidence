# A111 修前证据（2026-10-07 10:46:23，TCMS 引擎实例 43361 / job 2180 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：通用接口直发 hrm_attendance_leave 流程（不带 businessKey）：

```
POST /admin-api/bpm/process-instance/create {processDefinitionId: "hrm_attendance_leave:..."}
→ {"code": 0, "data": "486d5c2d-c1f9-11f1-8b75-fee45c6e4f05"}
```

请求（管理员取消该实例）：

```
DELETE /admin-api/bpm/process-instance/cancel-by-admin
  {"id": "486d5c2d-c1f9-11f1-8b75-fee45c6e4f05", "reason": "..."}
→ {"code": 500, "msg": "系统异常", "data": null}
```

服务器日志同刻堆栈原文：

```
java.lang.NumberFormatException: Cannot parse null string
	at java.base/java.lang.Long.parseLong(Long.java:672)
	at java.base/java.lang.Long.parseLong(Long.java:832)
	at cn.iocoder.yudao.module.hrm.service.attendance.record.listener.HrmAttendanceLeaveStatusListener.onEvent(HrmAttendanceLeaveStatusListener.java:29)
```

本轮复现 DB 对账：取消被回滚——ACT_RU_EXECUTION 该实例行仍在、ACT_HI_PROCINST
END_TIME_ 为 NULL（实例仍运行中，取消未生效）。用例断言「取消应成功 code=0」失败（判 FAIL）。

对照腿：带 businessKey 的正常请假流程取消/审批回写不受影响。
