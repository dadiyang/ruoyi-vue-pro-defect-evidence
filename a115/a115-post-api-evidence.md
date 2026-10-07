# A115 修后证据（2026-10-07 10:57:57，TCMS 引擎实例 43369 / job 2188 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（deleteProduct 调
deleteDevicePropertyData → DROP STABLE IF EXISTS）。

同一流程（载体 IOT-02 链产品 id=490）：

```
PUT /admin-api/iot/product/update-status?id=490&status=1   → code=0（发布，建超级表）
TDengine: SHOW STABLES LIKE 'product_property_490'          → rows=1（前置成立）
PUT /admin-api/iot/product/update-status?id=490&status=0   → code=0（撤销发布）
DELETE /admin-api/iot/product/delete?id=490                → code=0（删除成功）
MySQL: iot_product id=490 deleted=1                        → 软删生效
TDengine: SHOW STABLES LIKE 'product_property_490'          → rows=0（随删清理）
```

既有断言全部照旧通过：物模型属性/服务/事件三型嵌套读回、identifier 同产品查重钉
1050002002、page productId 过滤真生效、发布冻结防线钉 1050001003、撤销发布后删除读回等。
