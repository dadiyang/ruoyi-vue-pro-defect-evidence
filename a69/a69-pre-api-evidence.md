# A69 修前证据（2026-10-07 09:26:58，TCMS 引擎实例 43310 / job 2138 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

步骤（管理端装修模板，模板停用后删除）：

```
POST /admin-api/promotion/diy-template/create   {"name": "R15PRO复…"} → {"code":0,"data":195}
（创建时服务端自动生成「首页/我的」两个页面，template_id=195）
PUT  /admin-api/promotion/diy-template/use?id=<另一模板>   （停用本模板）
DELETE /admin-api/promotion/diy-template/delete?id=195     → {"code":0,"data":true}
```

DB 对账：

```
SELECT CAST(deleted AS UNSIGNED) FROM promotion_diy_template WHERE id=195
→ 1（模板已删）

SELECT COUNT(*) FROM promotion_diy_page WHERE template_id=195 AND deleted=0
→ 2（两个默认页残留，成为孤儿页）
```

孤儿页留在「装修页面」列表里，其所属模板已不存在；断言失败信息即
「删除模板后其默认页应级联删除: template_id=195 残留页数=2」。
