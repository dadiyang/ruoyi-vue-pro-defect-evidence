# A87 修前证据（2026-10-07 09:51:58，TCMS 引擎实例 43327 / job 2153 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：创建属性「R15PRD规G<戳>」及值 S/M/L；属性值 S 改名为「R15PRD规G<戳>S」。

请求（多规格 SPU 创建，SKU 规格名传空串、propertyId/valueId 合法）：

```
POST /admin-api/product/spu/create
{"name": "R15PRD空名<戳>", "specType": true, "skus": [{"name": "S空名",
  "properties": [{"propertyId": 142, "propertyName": "",
                  "valueId": 324, "valueName": ""}], …}]}
→ {"code": 0, "data": <spuId>}
```

C 端详情读回：

```
GET /app-api/product/spu/get-detail?id=<spuId>
skus[0].properties = [{"propertyId": 142, "propertyName": "", "valueId": 324, "valueName": ""}]
```

空规格名原样落库（不校验不回填）——H5 规格选择器按名渲染，选项显示空白。
