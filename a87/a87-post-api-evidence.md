# A87 修后证据（2026-10-07 09:53:17，TCMS 引擎实例 43328 / job 2154 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（validateSkuList 末尾以属性库名回填）。

同一请求（SKU 规格名传空串、propertyId/valueId 合法）：

```
POST /admin-api/product/spu/create → {"code": 0, "data": 3939}
```

C 端详情读回（回填生效）：

```
GET /app-api/product/spu/get-detail?id=3939
skus[0].properties = [{"propertyId": 143, "propertyName": "R15PRD规G337995",
                       "valueId": 327, "valueName": "R15PRD规G337995S"}]
```

propertyName/valueName 均被属性库权威名覆盖（属性库名创建时 @NotEmpty 保证非空）。

既有断言全部照旧通过：规格属性组合等值、正常传名回显、属性值改名回显、
改名撞名拒 1008004001、不存在/重复删除拒 1008004000、属性值软删等。
