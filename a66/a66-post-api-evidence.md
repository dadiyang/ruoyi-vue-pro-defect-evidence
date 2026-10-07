# A66 修后证据（2026-10-07 09:19:42，TCMS 引擎实例 43306 / job 2134 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（convert 去掉 setUserId(0L) 硬覆盖）。

同一请求（管理端新建评价，userId=968）：

```
POST /admin-api/product/comment/create
{"userId": 968, "orderItemId": 3763, "skuId": 4069, …}
→ {"code": 0, "data": true}
```

落库对账（DB）：

```
SELECT user_id,sku_id,spu_id,description_scores,benefit_scores,scores,content,visible
FROM product_comment WHERE order_item_id=3763 AND deleted=0
→ ["968", "4069", "3929", "5", "5", "5", "PRD-01自评…", "1"]
```

评价归属正确落到请求评价人；分页展示、C 端好评 tab、越权拒绝等其余断言全部照旧通过。
