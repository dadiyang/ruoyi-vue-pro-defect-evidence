# A115 修前证据（2026-10-07 10:56:45，TCMS 引擎实例 43368 / job 2187 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

流程（载体 IOT-02 链产品 id=489，带属性物模型）：

```
PUT /admin-api/iot/product/update-status?id=489&status=1   → code=0（发布，副作用建超级表）
TDengine: SHOW STABLES LIKE 'product_property_489'          → rows=1（前置成立）
PUT /admin-api/iot/product/update-status?id=489&status=0   → code=0（撤销发布）
DELETE /admin-api/iot/product/delete?id=489                → code=0（删除成功）
MySQL: iot_product id=489 deleted=1                        → 软删生效
TDengine: SHOW STABLES LIKE 'product_property_489'          → rows=1（表仍在！）
```

用例断言「产品删除后属性超级表不得残留」失败（判 FAIL）。

存量盘点（建卡当次现核）：现库 238 张 product_property_* 超级表后缀全部对应 deleted=1
软删产品，活跃产品名下 0 张——只增不减；整个 iot 模块 grep DROP STABLE/dropStable/dropSuperTable
零命中。
