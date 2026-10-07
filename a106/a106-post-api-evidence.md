# A106 修后证据（2026-10-07 10:42:45，TCMS 引擎实例 43360 / job 2179 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（operate-log/page 补
@CrmPermission READ 数据权限注解）。

同一请求（非负责人账号直调）：

```
GET /admin-api/crm/operate-log/page?pageNo=1&pageSize=20&bizType=2&bizId=<他人客户id>
→ {"code": 1020007001, "msg": "客户操作失败，原因：没有权限", "data": null}
```

受控拒绝复用 CRM 数据权限既有码 CRM_PERMISSION_DENIED(1_020_007_001)
（与跟进记录分页同款切面同款码）。

既有断言全部照旧通过：admin（负责人）查客户留痕恰 2 条（创建/更新 subType 精确、
action 含原名/新名与"客户等级"字段差异、操作人 userId=1、留痕时间不早于本轮起点）、
合同留痕恰 1 条含合同名、分页不混他载体行等。
