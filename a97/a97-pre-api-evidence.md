# A97 修前证据（2026-10-07 10:19:00，TCMS 引擎实例 43338 / job 2164 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：本轮现造供应商/账户/产品/单位→正常建单（明细带全必填）成功。

请求（明细缺 productUnitId，其余同合法载荷）：

```
POST /admin-api/erp/purchase-order/create
{"supplierId": ..., "accountId": ..., "orderTime": ..., "discountPercent": 0,
 "remark": "R15契约采购",
 "items": [{"productId": ..., "productPrice": 100, "count": 1, "taxPercent": 0}]}
→ {"code": 0, "msg": "", "data": 554}     ← 创建成功，订单 554 落库
```

Item 内声明的 @NotNull（productId/productUnitId/count）与 Schema requiredMode=REQUIRED
均不生效——外层 `private List<Item> items;` 缺 @Valid，嵌套校验不触发。
落库行 product_unit_id 非空仅因服务层从产品档案回填（ErpPurchaseOrderServiceImpl.java:160），
掩盖不了"声明必填却不校验"。用例断言「应 400 校验拒绝」失败（判 FAIL）。
