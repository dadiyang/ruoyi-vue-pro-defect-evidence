# A68 修前证据（2026-10-07 09:22:47，TCMS 引擎实例 43308 / job 2136 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

请求（管理端新建 SPU，配送方式填 3=虚拟配送——DeliveryTypeEnum 仅有 EXPRESS(1)/PICK_UP(2)）：

```
POST /admin-api/product/spu/create
{"name": "R14虚拟品…", "deliveryTypes": [3], "deliveryTemplateId": …, "skus": […]}
→ {"code": 0, "data": <spuId>}
```

保存成功、静默入库。该商品此后任何下单尝试都被拒（交易侧按请求 deliveryType 校验，
SPU 的 [3] 与任何合法请求配送方式都不匹配，TradeDeliveryPriceCalculator:60 拒「配送方式不正确」）——
商品在商城实际不可下单，但管理端全程无告警。
