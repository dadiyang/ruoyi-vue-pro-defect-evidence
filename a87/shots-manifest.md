# A87 证据清单（api 轨：静默数据质量缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a87-pre-api-evidence.md | 修前：多规格创建传空规格名，空名原样落库，C 端 get-detail 规格名空白 | TCMS 引擎实例 43327（job 2153，R57，2026-10-07 09:51:58，在役包不含本修复） |
| a87-post-api-evidence.md | 修后：同一创建请求，落库规格名被属性库权威名回填（propertyName/valueName 非空等值库名） | TCMS 引擎实例 43328（job 2154，R57，2026-10-07 09:53:17，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a87
