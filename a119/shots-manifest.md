# A119 证据清单（api 轨：顺序语义类缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a119-pre-api-evidence.md | 修前：top-senders 返回 messageCount 升序排列（最少 51 排第一），用例契约腿判 FAIL | TCMS 引擎实例 43370（job 2189，R57，2026-10-07 10:59:30，在役包不含本修复） |
| a119-post-api-evidence.md | 修后：同一端点返回 [79, 51] 降序，TOP 语义恢复 | TCMS 引擎实例 43372（job 2191，R57，2026-10-07 11:01:59，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a119
