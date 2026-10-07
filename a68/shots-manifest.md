# A68 证据清单（api 轨：保存校验缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a68-pre-api-evidence.md | 修前：SPU 保存 deliveryTypes=[3]（虚拟配送）返回 code=0 静默入库 | TCMS 引擎实例 43308（job 2136，R57，2026-10-07 09:22:47，在役包不含本修复） |
| a68-post-api-evidence.md | 修后：同一保存请求受控拒 code=400「请求参数不正确:配送方式不正确」；正常配送方式保存不受影响 | TCMS 引擎实例 43309（job 2137，R57，2026-10-07 09:24:10，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a68
