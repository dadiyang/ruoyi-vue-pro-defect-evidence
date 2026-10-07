# A47 修后证据（2026-10-07 09:05:23，TCMS 引擎实例 43301 / job 2129 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（MpOpenController 验签失败受控拒绝）。

同一请求（伪造验签参数 POST 推送）：

```
POST /admin-api/mp/open/wxr15071789748914133?signature=deadbeef&timestamp=1&nonce=2
Content-Type: application/xml
（消息体同上）
```

响应（HTTP 200，响应体为纯文本，无异常）：

```
非法请求
```

服务端日志窗口（同一请求，仅 WARN 一行，无堆栈）：

```
2026-10-07 09:05:23.961 [http-nio-18080-exec-6] WARN  c.i.y.m.mp.controller.admin.open.MpOpenController:89 - [handleMessage0][appId(wxr15071789748914133) 验签失败，拒绝推送请求]
```

与 GET 认证消息面行为一致：验签失败受控拒绝、不落 ERROR 堆栈。
