# A88 修后证据（2026-10-07 09:56:41，TCMS 引擎实例 43330 / job 2156 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（随机下界改取 randomMinPrice）。

同一活动（randomMinPrice=randomMaxPrice=300）帮砍一刀：

```
POST /app-api/promotion/bargain-help/create  {"recordId": <rid>}
→ {"code": 0, "data": 300}
```

DB 对账：promotion_bargain_record.bargain_price = 5700（6000-300）。

对照与连带：
- 原三值相等活动（randomMin=randomMax=底价=1000）五刀仍恒 1000、砍至底价 SUCCESS——
  修复对该配置无影响（randomInt(1000,1001) 前后一致）；
- 底价下单 pay_price=1010、orderId 回写、库存联动 sku=9/act=9、
  重复参与 1013013001/自砍 1013014001/重复助力 1013014004/成功后助力 1013014000/
  重复下单 1013013005 等既有断言全部照旧通过。
