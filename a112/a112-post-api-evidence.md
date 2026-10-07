# A112 修后证据（2026-10-07 10:51:08，TCMS 引擎实例 43364 / job 2183 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（create 回填空列表＋分页渲染判空）。

同一请求（创建省略 contactIds/businessIds 后分页）：

```
POST /admin-api/crm/follow-up-record/create（省略两字段）→ {"code": 0, "data": 372}
GET /admin-api/crm/follow-up-record/page?pageNo=1&pageSize=50&bizType=2&bizId=<客户id>
→ {"code": 0, ...}  正常出页，新行 contacts/businesses 为空数组渲染
```

DB 对账（create 侧回填空列表）：id=372 → contact_ids/business_ids 落空串
（LongListTypeHandler 以逗号串存储，空列表=空串；读回为空列表），
对照修前 id=366 的 NULL。

既有断言全部照旧通过：四类载体跟进筛选纯净（条数与现造数一致）、缺 bizId 受控拒绝 400、
无数据权限用户受控拒绝 1020007001、收尾清理读回等。
