# A102 修后证据（2026-10-07 10:37:02，TCMS 引擎实例 43356 / job 2175 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（切面 bizId 判空）。

同一请求（缺 bizId）：

```
GET /admin-api/crm/follow-up-record/page?pageNo=1&pageSize=10&bizType=2
→ {"code": 400, "msg": "数据权限校验失败，原因：请求缺少参数 (#pageReqVO.bizId)", "data": null}
```

既有断言全部照旧通过：四类载体（线索/客户/联系人/商机）跟进筛选纯净（条数与现造数一致、
不混他载体）、无数据权限用户查跟进分页受控拒绝 1020007001、收尾清理读回等。
