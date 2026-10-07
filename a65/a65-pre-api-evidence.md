# A65 修前证据（2026-10-07 09:14:21，TCMS 引擎实例 43303 / job 2131 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：流程定义（示例用 HR 请假审批流程 hrm_attendance_leave）配置
「允许撤销审批中的申请」＝关（allowCancelRunningProcess=false），并有一条审批中的申请。

取消请求：

```
PUT /admin-api/hrm/portal/attendance/leave/cancel
{"id": 31, "reason": "R15禁取消验证HRM-13"}
```

响应（HTTP 200，业务码）：

```json
{"code": 1009004005, "msg": "流程取消失败，该流程不允许取消", "data": null}
```

同一业务码 1009004005 同时是「发起流程失败，你没有权限发起该流程」
（bpm ErrorCodeConstants.java:42-43 两常量同值）——客户端拿到 1009004005
无法区分「这个流程不允许取消」与「你没有权限发起」。
