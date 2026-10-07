# A69 证据清单（api 轨：级联删除缺陷，以 DB 对账替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a69-pre-api-evidence.md | 修前：删除模板成功（deleted=1），其自动生成的「首页/我的」两页残留（deleted=0 孤儿页） | TCMS 引擎实例 43310（job 2138，R57，2026-10-07 09:26:58，在役包不含本修复） |
| a69-post-api-evidence.md | 修后：删除模板后其页面清零（级联删除），启用切换/使用中拒删等既有断言照旧 | TCMS 引擎实例 43311（job 2139，R57，2026-10-07 09:28:15，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a69
