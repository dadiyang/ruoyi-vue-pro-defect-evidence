# A99 修后证据（2026-10-07 10:33:53，TCMS 引擎实例 43354 / job 2173 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（validateLedgerPeriod 补初始化判空）。

同一请求（本轮现造未初始化账套 accountSetId=428）：

```
GET /admin-api/fms/report/balance-sheet/get?accountSetId=428&startMonth=2026-10&endMonth=2026-10
→ {"code": 1052100005, "msg": "账套尚未完成初始化", "data": null}
```

受控拒绝复用模块既有错误码 ACCOUNT_SET_NOT_INITIALIZED(1_052_100_005)
（结账/参数域 FmsClosingPeriodServiceImpl:117/506 等既有同款守卫）。

既有断言全部照旧通过：初始化账套资产负债表 code=0 含模板科目行、不存在账套钉 1052100000、
mes 三分页计数对账、wms 仓库/入库单面自造对账、pms 项目面自造对账等。
