# A91 证据清单（api 轨：视图与执行层口径不一致缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a91-pre-api-evidence.md | 修前：角色只授按钮 39（不含祖先）时，/system/dept/list 放行（code=0）但 get-permission-info 的 permissions=[] | TCMS 引擎实例 43331（job 2157，R57，2026-10-07 09:59:29，在役包不含本修复） |
| a91-post-api-evidence.md | 修后：同一授权形态下 permissions=["system:dept:query"]，视图与执行层一致；祖先链授权/撤权失效等既有断言照旧 | TCMS 引擎实例 43333（job 2159，R57，2026-10-07 10:04:26，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a91
