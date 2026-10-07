# A84 修前证据（2026-10-07 09:48:32，TCMS 引擎实例 43325 / job 2151 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：新会员钱包充值 100（mock 回调到账）→ 钱包支付消费 100
（pay_wallet_transaction 落一条 price=-100 的支出流水）。

请求（流水汇总，窗口覆盖本轮）：

```
GET /app-api/pay/wallet-transaction/get-summary?createTime=2026-10-07 00:00:00,2026-10-08 00:00:00
```

响应（HTTP 200）：

```json
{"code": 0, "data": {"totalExpense": -100, "totalIncome": 200}}
```

DB 对账：

```
SELECT IFNULL(SUM(price),0) FROM pay_wallet_transaction WHERE wallet_id=427 AND price<0 AND deleted=0
→ -100
```

接口把负值流水直接求和返回 -100。而钱包级累计支出（pay_wallet.total_expense）由
消费路径按正值累加维护（PayWalletMapper.updateWhenConsumption：total_expense + price），
同一"累计支出"两个口径符号相反。
