# A98 证据清单（api 轨：错误码语义类缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a98-pre-api-evidence.md | 修前：截断 JSON 请求体返回 code=500「系统异常」 | TCMS 引擎实例 43347（job 2166，R57，2026-10-07 10:22:18，在役包不含本修复） |
| a98-post-api-evidence.md | 修后：同一请求 code=400「请求参数格式错误:Unexpected end-of-input…」 | TCMS 引擎实例 43348（job 2167，R57，2026-10-07 10:24:39，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a98
