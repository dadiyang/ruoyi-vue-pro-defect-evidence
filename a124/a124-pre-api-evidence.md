# A124 修前证据（2026-10-07 11:06:41，TCMS 引擎实例 43373 / job 2192 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

请求（建券模板，takeType=9 枚举外；枚举仅 1 直接领取/2 指定发放/3 新人券）：

```
POST /admin-api/promotion/coupon-template/create
{"name":"R15PRO新人X...","totalCount":100,"takeLimitCount":1,"usePrice":0,
 "takeType":9,"productScope":1,"discountType":1,"discountPrice":50,...}
→ {"code": 0, "data": <模板id>}
```

服务器日志同刻 INSERT 实参（脏行落库坐实）：

```
2026-10-07 11:06:41.421 DEBUG CouponTemplateMapper.insert - ==> Parameters:
R15PRO新人X...(String), 0(Integer), 100(Integer), 1(Integer), 9(Integer), ...
```

后果链（建卡已三源互证）：该脏模板 C 端领取被下游闸门拒 1013004005
（CouponServiceImpl.validateCouponTemplateCanTake 恒按 USER(1) 校验）——谁都领不了；
管理端券模板列表 takeType 列显示空白（字典 promotion_coupon_take_type 映射不到）。

用例断言「枚举外创建应受控拒绝 400」失败（判 FAIL，实测 code=0）。
