# A72 修前证据（2026-10-07 09:34:01，TCMS 引擎实例 43314 / job 2142 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：用通用接口发起 oa_leave 流程（不经请假业务单，无 businessKey）：

```
POST /admin-api/bpm/process-instance/create
{"processDefinitionId": "oa_leave:<版本>:<部署id>", "variables": {"reason": "R15BPM03A72", "day": 1},
 "startUserSelectAssignees": {}}
→ {"code": 0, "data": "<流程实例id>"}
```

取消请求：

```
DELETE /admin-api/bpm/process-instance/cancel-by-admin
{"id": "<流程实例id>", "reason": "BPM-03 A72 无businessKey取消"}
```

响应（HTTP 200，业务码 500）：

```json
{"code": 500, "msg": "系统异常", "data": null}
```

服务端日志窗口（同一请求，ERROR 级堆栈）：

```
java.lang.NumberFormatException: Cannot parse null string
	at cn.iocoder.yudao.module.bpm.service.oa.listener.BpmOALeaveStatusListener.onEvent(BpmOALeaveStatusListener.java:29)
```

后果：取消事务回滚，实例停留在运行中；再次取消同样 500——流程实例永久卡死，
只能靠数据库手术清理（引擎本轮实测：修前遗留实例在修复部署后才得已取消清净）。
