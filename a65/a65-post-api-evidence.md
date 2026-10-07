# A65 修后证据（2026-10-07 09:15:48，TCMS 引擎实例 43304 / job 2132 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（PROCESS_INSTANCE_CANCEL_FAIL_NOT_ALLOW 改独立码）。

同一取消请求（流程定义仍配置「不允许撤销审批中的申请」）：

```
PUT /admin-api/hrm/portal/attendance/leave/cancel
{"id": 31, "reason": "R15禁取消验证HRM-13"}
→ {"code": 1009004010, "msg": "流程取消失败，该流程不允许取消", "data": null}
```

恢复「允许撤销」配置后同一申请取消成功（正常链路不受影响）：

```
PUT /admin-api/hrm/portal/attendance/leave/cancel
{"id": 31, "reason": "R15取消HRM-13C"}
→ {"code": 0, "msg": "", "data": true}
```

「无权限发起该流程」仍为 1009004005，两语义错误码不再冲突。
