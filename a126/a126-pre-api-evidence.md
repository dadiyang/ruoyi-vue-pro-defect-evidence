# A126 修前证据（2026-10-07 11:11:32，TCMS 引擎实例 43375 / job 2194 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：admin 创建演示订单（支付单属主=admin，PayDemoOrderServiceImpl.java:94
setUserId=登录 admin＋ADMIN 型），单据待支付（status=0）；另备一个与该单
无任何关系的会员账号登录取令牌。

请求（会员令牌直提他人支付单）：

```
POST /app-api/pay/order/submit {"id": <admin属主支付单id>, "channelCode": "mock"}
→ {"code": 0, "data": {"status": 10, ...}}
```

即：非属主账号把他人待支付单提交成已支付（支付流水 pay_order_extension 落库）——
越权提交当场坐实。对照：同一会员令牌查询该单（GET /app-api/pay/order/get）返回
data=null（查询侧已核对属主，AppPayOrderController.java:67-71）。

用例断言「应受控拒绝 1007002000」失败（判 FAIL）。

补充（建卡当次接口直证）：钱包渠道提交强制用提交人自己的钱包
（WalletPayClient 按 walletId 扣款），扣他人钱包未证实，资金面风险不外推。
