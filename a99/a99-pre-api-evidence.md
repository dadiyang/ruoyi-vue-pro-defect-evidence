# A99 修前证据（2026-10-07 10:32:38，TCMS 引擎实例 43353 / job 2172 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，本单修前腿以 A99-revert 构建部署
（在役分支临时回退本修复后构建，判定腿与修后腿同载体同载荷）。

前置：本轮现造账套（companyCode=IND03PR…，仅 create 未走初始化，start_time=NULL）。

请求：

```
GET /admin-api/fms/report/balance-sheet/get?accountSetId=426&startMonth=2026-10&endMonth=2026-10
→ {"code": 500, "msg": "系统异常", "data": null}
```

服务器日志同刻堆栈原文：

```
2026-10-07 10:32:37.859 [http-nio-18080-exec-2] ERROR c.i.y.f.web.core.handler.GlobalExceptionHandler:349 - [defaultExceptionHandler]
java.lang.NullPointerException: temporal
	at java.base/java.util.Objects.requireNonNull(Objects.java:259)
	at java.base/java.time.YearMonth.from(YearMonth.java:257)
	at cn.iocoder.yudao.module.fms.service.ledger.FmsLedgerServiceImpl.validateLedgerPeriod(FmsLedgerServiceImpl.java:1414)
	at cn.iocoder.yudao.module.fms.service.ledger.FmsLedgerServiceImpl.buildContext(FmsLedgerServiceImpl.java:403)
```

对照同请求族：不存在账套受控 1052100000、已初始化账套 code=0 正常出表，
唯独「存在但未初始化」崩溃。用例断言「应受控拒绝 1052100005」失败（判 FAIL）。
