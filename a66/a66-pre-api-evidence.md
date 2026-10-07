# A66 修前证据（2026-10-07 09:18:19，TCMS 引擎实例 43305 / job 2133 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

请求（管理端新建评价，评价人 userId=968 为已注册会员——该会员正是本订单项的买家）：

```
POST /admin-api/product/comment/create
{"userId": 968, "orderItemId": 3763, "skuId": 4069, "userNickname": "用户979293",
 "userAvatar": "…", "descriptionScores": 5, "benefitScores": 5,
 "content": "PRD-01自评…", "picUrls": []}
→ {"code": 0, "data": true}
```

落库对账（DB）：

```
SELECT user_id FROM product_comment WHERE order_item_id=3763 AND deleted=0
→ user_id = 0
```

请求里必填的「评价人」被服务端丢弃，评价归属成未知账号（user_id=0）：
会员侧「我的评价」查不到、按用户筛选/统计均漏这条评价。
