# A70 修后证据（2026-10-07 09:31:32，TCMS 引擎实例 43313 / job 2141 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（两处 Assert.notNull 改受控抛业务码）。

同一请求（会员 A 令牌，addressId 为 B 的地址）：

```
POST /app-api/trade/order/create
{"pointStatus": false, "deliveryType": 1, "addressId": <B的地址编号>,
 "items": [{"skuId": …, "count": 1}], "remark": "TRD-03越权"}
→ {"code": 1011000117, "msg": "交易订单创建失败，收货地址不存在", "data": null}
```

对照（同轮，本人地址正常下单不受影响）：

```
POST /app-api/trade/order/create（本人 addressId）→ {"code": 0, "data": {"id": 3677, …}}
```

快照固化、结算一致、改源后新单取新资料等既有断言全部照旧通过。
