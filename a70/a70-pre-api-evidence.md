# A70 修前证据（2026-10-07 09:30:05，TCMS 引擎实例 43312 / job 2140 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：会员 B（13970000003）创建专属收货地址；会员 A 用该地址编号下单。

请求（会员 A 令牌，addressId 为 B 的地址）：

```
POST /app-api/trade/order/create
{"pointStatus": false, "deliveryType": 1, "addressId": <B的地址编号>,
 "items": [{"skuId": …, "count": 1}], "remark": "TRD-03越权"}
```

响应（HTTP 200，业务码 500）：

```json
{"code": 500, "msg": "系统异常", "data": null}
```

服务端日志窗口（同一请求，ERROR 级全堆栈）：

```
2026-10-07 09:30:05.450 [http-nio-18080-exec-7] ERROR c.i.y.f.web.core.handler.GlobalExceptionHandler:342 - [defaultExceptionHandler]
java.lang.IllegalArgumentException: 收件人(960)的地址，不能为空
	at cn.iocoder.yudao.module.trade.service.price.calculator.TradeDeliveryPriceCalculator.calculateExpress(TradeDeliveryPriceCalculator.java:91)
	at cn.iocoder.yudao.module.trade.service.price.calculator.TradeDeliveryPriceCalculator.calculate(TradeDeliveryPriceCalculator.java:67)
	at cn.iocoder.yudao.module.trade.service.order.TradeOrderUpdateServiceImpl.calculatePrice(TradeOrderUpdateServiceImpl.java:180)
```

即：addressApi.getAddress(addressId, userId) 对他人地址返回 null（会员模块按归属过滤），
Assert.notNull 把这一可预期的输入当作未预期异常落 500 兜底。
