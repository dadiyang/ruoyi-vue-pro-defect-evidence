# A47 修前证据（2026-10-07 09:02:56，TCMS 引擎实例 43299 / job 2127 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，**临时回退验签修复**（即上游现尖端行为）。

请求（对已配置公众号 appId 伪造验签参数推送 XML 消息）：

```
POST /admin-api/mp/open/wxr15071789748914133?signature=deadbeef&timestamp=1&nonce=2
Content-Type: application/xml

<xml><ToUserName><![CDATA[r15]]></ToUserName><FromUserName><![CDATA[oR15]]></FromUserName>
<CreateTime>1</CreateTime><MsgType><![CDATA[text]]></MsgType><Content><![CDATA[hi]]></Content></xml>
```

响应（HTTP 200，业务码 500）：

```json
{"code": 500, "msg": "系统异常", "data": null}
```

服务端日志窗口（同一请求，ERROR 级全堆栈）：

```
2026-10-07 09:02:56.763 [http-nio-18080-exec-6] INFO  ApiAccessLogInterceptor:51 - [preHandle][开始请求 URL(/admin-api/mp/open/wxr15071789748914133) 参数("<xml>...")]
2026-10-07 09:02:56.776 [http-nio-18080-exec-6] ERROR c.i.y.f.web.core.handler.GlobalExceptionHandler:342 - [defaultExceptionHandler]
java.lang.RuntimeException: java.lang.IllegalArgumentException: 非法请求
	at cn.iocoder.yudao.framework.tenant.core.util.TenantUtils.execute(TenantUtils.java:59)
	at cn.iocoder.yudao.module.mp.controller.admin.open.MpOpenController.handleMessage(MpOpenController.java:57)
```

对照：GET 认证消息面（checkSignature，:70-83）验签失败时受控返回文本「非法请求」，不落异常——POST 推送面缺同一处理。
