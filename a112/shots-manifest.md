# A112 证据清单（api 轨：崩溃类缺陷，以接口响应原文＋服务器日志堆栈＋DB 对账替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a112-pre-api-evidence.md | 修前：创建跟进省略 contactIds/businessIds（列落 NULL）后分页返回 code=500「系统异常」＋日志 NPE 堆栈（Controller:95）＋DB 对账 contact_ids=NULL | TCMS 引擎实例 43363（job 2182，R57，2026-10-07 10:49:49，在役包不含本修复）＋/home/irons/logs/yudao-server.log＋业务库对账 |
| a112-post-api-evidence.md | 修后：同一请求 code=0 正常出页、该行 contacts/businesses 空渲染＋DB 对账新行落空串（回填空列表） | TCMS 引擎实例 43364（job 2183，R57，2026-10-07 10:51:08，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a112
