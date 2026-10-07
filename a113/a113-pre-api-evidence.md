# A113 修前证据（2026-10-07 10:52:55，TCMS 引擎实例 43365 / job 2184 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

请求（建产品省略 productKey；其余字段同合法载荷）：

```
POST /admin-api/iot/product/create
{"name":"回归产品无Key001","categoryId":508,"deviceType":0,"netType":0,
 "protocolType":"emqx","serializeType":"json","registerEnabled":false}
→ {"code": 500, "msg": "系统异常", "data": null}
```

服务器日志同刻堆栈原文：

```
2026-10-07 10:52:55.488 [http-nio-18080-exec-1] ERROR c.i.y.f.web.core.handler.GlobalExceptionHandler:349 - [defaultExceptionHandler]
java.lang.NullPointerException: Cannot invoke "String.toLowerCase()" because "<parameter1>" is null
	at cn.iocoder.yudao.module.iot.dal.mysql.product.IotProductMapper.selectByProductKey(IotProductMapper.java:38)
```

对照腿：显式传 productKey 创建 code=0 成功、同 Key 重复创建受控拒 1050001001。
用例断言「应受控拒绝 400」失败（判 FAIL）。
