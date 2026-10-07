# A119 修前证据（2026-10-07 10:59:30，TCMS 引擎实例 43370 / job 2189 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

请求：

```
GET /admin-api/im/manager/statistics/top-senders
→ {"code": 0, "data": [
    {"userId": 1,   "nickname": "芋道源码",  "messageCount": 51},
    {"userId": 254, "nickname": "IM机器人1", "messageCount": 79}]}
```

消息最少的人（51）排第一——返回顺序与消息数无关（本例实测恰为升序，散列序无规律）。
SQL 已 ORDER BY messageCount DESC（ImStatisticsManagerMapper.java:186 LIMIT 10），
丢序发生在服务层 convertMap 默认 HashMap 收集（ImStatisticsManagerServiceImpl:112-114）。

用例断言「messageCount 倒序且 ≤10 条」失败（判 FAIL，实测 cnts=[51, 79]）。
