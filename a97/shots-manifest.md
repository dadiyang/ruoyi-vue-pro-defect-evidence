# A97 证据清单（api 轨：校验缺失类缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a97-pre-api-evidence.md | 修前：明细缺 productUnitId 建采购订单返回 code=0（误建单 554 落库） | TCMS 引擎实例 43338（job 2164，R57，2026-10-07 10:19:00，在役包不含本修复） |
| a97-post-api-evidence.md | 修后：同一请求 400「请求参数不正确:产品单位单位不能为空」；连带 ERP-01~06/09 全过 | TCMS 引擎实例 43339（job 2165，R57，2026-10-07 10:20:35，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a97
