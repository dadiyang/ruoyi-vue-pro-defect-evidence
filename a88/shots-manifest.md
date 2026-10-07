# A88 证据清单（api 轨：配置不生效缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a88-pre-api-evidence.md | 修前：randomMinPrice=randomMaxPrice=300 的活动，一刀砍价金额实测 826（落 [301,1000] 随机区间） | TCMS 引擎实例 43329（job 2155，R57，2026-10-07 09:55:19，在役包不含本修复） |
| a88-post-api-evidence.md | 修后：同一活动一刀恒 300、记录价 6000→5700；原三值相等活动仍恒 1000，SUCCESS/下单/库存联动照旧 | TCMS 引擎实例 43330（job 2156，R57，2026-10-07 09:56:41，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a88
