# A111 修后证据（2026-10-07 10:47:54，TCMS 引擎实例 43362 / job 2181 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（监听器 businessKey 判空跳过）。

同一请求（通用发起无 businessKey 实例后管理员取消）：

```
POST /admin-api/bpm/process-instance/create → {"code": 0, "data": "7ebeb25c-c1f9-11f1-9993-fee45c6e4f05"}
DELETE /admin-api/bpm/process-instance/cancel-by-admin {"id": "7ebeb25c-..."}
→ {"code": 0, "msg": "", "data": true}
```

实例达取消终态（status=4，用例断言通过）。监听器日志受控跳过：

```
2026-10-07 10:47:53.922 WARN c.i.y.m.h.s.a.r.l.HrmAttendanceLeaveStatusListener:33 - [onEvent][流程实例(39dfbd6f-...) 无 businessKey，跳过请假申请状态回写]
2026-10-07 10:47:54.017 WARN c.i.y.m.h.s.a.r.l.HrmAttendanceLeaveStatusListener:33 - [onEvent][流程实例(486d5c2d-...) 无 businessKey，跳过请假申请状态回写]
```

（第二条即修前腿遗留的卡死实例，修复部署后用例残留清净腿正常取消。）

既有断言全部照旧通过：考勤组重名拒/假日重复拒/补卡出窗拒/请假 BPM 审批通过联动
approvalStatus=2/月统计 leaveDays=1.00 迟到清零/重叠请假钉 1050300031/清场读回等。
