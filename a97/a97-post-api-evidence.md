# A97 修后证据（2026-10-07 10:20:35，TCMS 引擎实例 43339 / job 2165 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（5 个 SaveReqVO items 补 @Valid）。

同一请求（明细缺 productUnitId）：

```
POST /admin-api/erp/purchase-order/create  （items[0] 无 productUnitId）
→ {"code": 400, "msg": "请求参数不正确:产品单位单位不能为空", "data": null}
```

（msg 中"产品单位单位"为源码 @NotNull message 原文，本 PR 未改动文案。）

既有断言全部照旧通过：正常建单（带全必填）3 明细行金额对账、DB 明细行对账、
未审核单建入库拒 1030101006、重复审核拒 1030101003、入库单创建与 supplierId 复制对账等。

连带验证（同 job 2165，创建这 5 类实体的既有 ERP 用例全过，必填载荷不受波及）：
ERP-01 实例 43340、ERP-02 43341、ERP-03 43344、ERP-04 43342、ERP-05 43345、
ERP-06 43346、ERP-09 43343——全部 PASS。
