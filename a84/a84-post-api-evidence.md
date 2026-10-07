# A84 修后证据（2026-10-07 09:49:49，TCMS 引擎实例 43326 / job 2152 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（支出汇总改 SUM(-price)）。

同一请求（流水汇总，窗口覆盖本轮）：

```
GET /app-api/pay/wallet-transaction/get-summary?createTime=2026-10-07 00:00:00,2026-10-08 00:00:00
→ {"code": 0, "data": {"totalExpense": 100, "totalIncome": 200}}
```

totalExpense=100 为正值幅度，等于 DB 负值支出 Σ（-100）的相反数，
与钱包级 pay_wallet.total_expense 的正值语义一致。

既有断言全部照旧通过：充值到账余额增、钱包支付扣减流水（price=-100 明细仍为负值不变）、
余额不足拒 1007007001、余额=Σ流水对账等。
