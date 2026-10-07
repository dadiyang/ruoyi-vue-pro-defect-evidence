# A88 修前证据（2026-10-07 09:55:19，TCMS 引擎实例 43329 / job 2155 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

活动配置：起始价 6000、底价 bargainMinPrice=1000、
randomMinPrice=300、randomMaxPrice=300（按 DO 注释语义，每次帮砍应恒砍 300）。

请求（好友帮砍一刀）：

```
POST /app-api/promotion/bargain-help/create  {"recordId": <rid>}
→ {"code": 0, "data": 826}
```

砍价金额 826 ≠ 配置的 300。根因：calculateReducePrice 随机下界误取底价——

```java
Integer reducePrice = MathUtil.randomInt(activity.getBargainMinPrice(),   // =1000
        activity.getRandomMaxPrice() + 1);                                 // =301
```

randomInt(1000, 301) 经 hutool 内部交换参数后落 [301,1000] 随机区间（实测 826 即区间内值）；
randomMinPrice 字段在全代码中零读取。
