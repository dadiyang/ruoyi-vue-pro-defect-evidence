# A124 修后证据（2026-10-07 11:07:58，TCMS 引擎实例 43374 / job 2193 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（CouponTemplateBaseVO.takeType
补 @InEnum(CouponTakeTypeEnum.class)，枚举已实现 ArrayValuable）。

同一请求（takeType=9 枚举外）：

```
POST /admin-api/promotion/coupon-template/create（同上）
→ {"code": 400, "msg": "请求参数不正确:必须在指定范围 [1, 2, 3]", "data": null}
```

日志对账：该请求（11:07:58.081 进入）无对应 INSERT——脏行不再落库。

对照腿（合法枚举值不受影响）：takeType=2（指定发放）创建 code=0 成功，
其 App 领取仍按既有语义受控拒绝 1013004005（App 领取恒按 USER(1) 校验）。

既有断言全部照旧通过：DATE 缺 validStartTime 钉 400＋报文、TERM end<start 下游防线、
PERCENT 缺上限钉 400＋合法创建反证、新人券合法创建与回显等。
