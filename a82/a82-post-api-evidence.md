# A82 修后证据（2026-10-07 09:43:38，TCMS 引擎实例 43322 / job 2148 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（空串条件改 apply 原生比较）。

同一请求（建频道→素材→群发后拉取）：

```
GET /admin-api/im/channel/message/pull?minId=0&size=200
→ {"code": 0, "data": [{"id": 58, "channelId": 58, "materialId": 58, "type": 125,
    "content": "{\"materialId\": 58, \"channelId\": 58, …}", "receiptStatus": 1, …}]}
```

内容级命中本轮推送：channelId/materialId 相符、type=125（素材卡片）、未读态 receiptStatus=1；
标记已读后再次拉取转 receiptStatus=2。

既有断言全部照旧通过：建频道/重复 code 拒 1040810001/素材 CRUD/群发/不存在素材拒 1040810010/
有素材删频道拒 1040810002/已推送删素材拒 1040810011 等。
