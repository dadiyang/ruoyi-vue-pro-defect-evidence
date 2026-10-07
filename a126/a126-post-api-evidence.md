# A126 修后证据（2026-10-07 11:13:54，TCMS 引擎实例 43380 / job 2195 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（AppPayOrderController
.submitPayOrder 补属主校验，与查询侧同款防线）。

同一请求（会员令牌提交 admin 属主待支付单 id=4603）：

```
POST /app-api/pay/order/submit {"id": 4603, "channelCode": "mock"}
→ {"code": 1007002000, "msg": "支付订单不存在", "data": null}
```

受控拒绝复用既有码 PAY_ORDER_NOT_FOUND(1_007_002_000)；被拒后该单仍待支付
（status=0，未被越权支付，用例断言通过）。

对照腿（属主通道不受影响）：admin（属主）经 admin-api 提交同一流程的支付单
4602 code=0 status=10；二次提交照旧拒 1007002002「订单已支付，请刷新页面」。

既有断言全部照旧通过：重复支付幂等（状态/金额不变、拓展表仅一条成功痕迹）、
PAY-01/07/08/11/14 五例（演示单 mock 支付腿改属主 admin-api 提交通道后）全绿。
