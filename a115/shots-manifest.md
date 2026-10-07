# A115 证据清单（api 轨：资源残留类缺陷，以接口调用原文＋TDengine 查表对账替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a115-pre-api-evidence.md | 修前：产品发布建超级表后删除产品，SHOW STABLES LIKE 'product_property_489' 仍 cnt=1（表残留） | TCMS 引擎实例 43368（job 2187，R57，2026-10-07 10:56:45，在役包不含本修复）＋TDengine REST 对账 |
| a115-post-api-evidence.md | 修后：同一流程删除产品后 SHOW STABLES 计数 0（超级表随删） | TCMS 引擎实例 43369（job 2188，R57，2026-10-07 10:57:57，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a115
