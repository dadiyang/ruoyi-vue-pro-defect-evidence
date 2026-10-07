# A66 证据清单（api 轨：落库数据缺陷，以接口请求＋DB 行对账替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a66-pre-api-evidence.md | 修前：请求 userId=968 建评价，DB 行 user_id=0（未知账号） | TCMS 引擎实例 43305（job 2133，R57，2026-10-07 09:18:19，在役包不含本修复） |
| a66-post-api-evidence.md | 修后：同一请求 userId=968，DB 行 user_id=968 | TCMS 引擎实例 43306（job 2134，R57，2026-10-07 09:19:42，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a66
