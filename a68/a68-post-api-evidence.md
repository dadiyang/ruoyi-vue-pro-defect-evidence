# A68 修后证据（2026-10-07 09:24:10，TCMS 引擎实例 43309 / job 2137 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（SpuSaveReqVO.deliveryTypes 加 @InEnum(DeliveryTypeEnum)）。

同一保存请求（deliveryTypes=[3]）：

```
POST /admin-api/product/spu/create
{"name": "R14虚拟品…", "deliveryTypes": [3], …}
→ {"code": 400, "msg": "请求参数不正确:配送方式不正确", "data": null}
```

对照（同轮，正常配送方式保存不受影响）：

```
deliveryTypes=[1] → {"code": 0, "data": 3932}
deliveryTypes=[2] → {"code": 0, "data": 3933}
```

下单侧防线行为不变：正常快递品按 deliveryType=3 下单仍被请求侧校验拒 400「配送方式不正确」；
快递发货、自提核销、错误物流公司拒绝等既有断言全部照旧通过。
