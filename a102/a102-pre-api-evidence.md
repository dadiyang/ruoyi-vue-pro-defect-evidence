# A102 修前证据（2026-10-07 10:35:49，TCMS 引擎实例 43355 / job 2174 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

请求（缺 bizId，其余同合法载荷）：

```
GET /admin-api/crm/follow-up-record/page?pageNo=1&pageSize=10&bizType=2
→ {"code": 500, "msg": "系统异常", "data": null}
```

服务器日志同刻堆栈原文：

```
2026-10-07 10:35:48.685 [http-nio-18080-exec-2] ERROR c.i.y.f.web.core.handler.GlobalExceptionHandler:349 - [defaultExceptionHandler]
java.lang.NullPointerException: Cannot invoke "Object.toString()" because "<local5>" is null
	at cn.iocoder.yudao.module.crm.framework.permission.core.aop.CrmPermissionAspect.doBefore(CrmPermissionAspect.java:66)
```

对照腿：带 bizId 同端点 code=0 正常返回——与数据无关，缺参必炸。
用例断言「应受控拒绝 400」失败（判 FAIL）。
