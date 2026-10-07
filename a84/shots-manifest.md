# A84 证据清单（api 轨：展示语义缺陷，以接口响应原文＋DB 对账替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a84-pre-api-evidence.md | 修前：流水汇总 get-summary 返回 totalExpense=-100（负数，与钱包级正值语义不符） | TCMS 引擎实例 43325（job 2151，R57，2026-10-07 09:48:32，在役包不含本修复） |
| a84-post-api-evidence.md | 修后：同一汇总返回 totalExpense=100（正值幅度），totalIncome=200 照旧 | TCMS 引擎实例 43326（job 2152，R57，2026-10-07 09:49:49，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a84
