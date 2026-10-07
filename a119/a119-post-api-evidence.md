# A119 修后证据（2026-10-07 11:01:59，TCMS 引擎实例 43372 / job 2191 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（getTopSenderCountMap 改
LinkedHashMap 收集保持 SQL DESC 序）。

同一请求：

```
GET /admin-api/im/manager/statistics/top-senders
→ {"code": 0, "data": [
    {"userId": 254, "nickname": "IM机器人1", "messageCount": 79},
    {"userId": 1,   "nickname": "芋道源码",  "messageCount": 51}]}
```

降序恢复（79 在前），TOP 语义成立。用例契约腿「messageCount 倒序且 ≤10 条」通过。

既有断言全部照旧通过：概览今日计数、消息趋势（今日群线增量）、类型分布增量、
群规模分布 1-9 人桶增量、days 越界(0/91)钉 400、prelude 残留清净与清场读回等。
