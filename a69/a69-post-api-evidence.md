# A69 修后证据（2026-10-07 09:28:15，TCMS 引擎实例 43311 / job 2139 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（deleteDiyTemplate 级联删页＋事务）。

同一流程（创建模板自动生成「首页/我的」→ 停用 → 删除）：

```
DELETE /admin-api/promotion/diy-template/delete?id=197 → {"code":0,"data":true}
```

DB 对账：

```
SELECT COUNT(*) FROM promotion_diy_page WHERE template_id=197 AND deleted=0
→ 0（默认页随模板级联删除，无孤儿页残留）
```

既有断言全部照旧通过：使用中删除拒 1013017002、停用后删除成功落 deleted 位、
已删再删拒 1013017000、启用切换 used 翻转等。
