# A74 修前证据（2026-10-07 09:38:32，TCMS 引擎实例 43317 / job 2145 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

请求（管理端，向不存在的站内信模板编码发送）：

```
POST /admin-api/system/notify-template/send-notify
{"templateCode": "sys03_none_<戳>", "templateParams": {"name": "…"},
 "userId": 1, "userType": 2}
```

响应（HTTP 200，业务码为公告域错误码）：

```json
{"code": 1002008001, "msg": "当前通知公告不存在", "data": null}
```

1002008001 属于「通知公告」域（NOTICE_NOT_FOUND）；站内信模板域已有在位码
NOTIFY_TEMPLATE_NOT_EXISTS=1002026000「站内信模版不存在」（模板增删改查即用此码），
发送路径却误抛公告码——客户端按码分支会把它当公告问题处理。
