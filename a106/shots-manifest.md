# A106 证据清单（api 轨：越权类缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a106-pre-api-evidence.md | 修前：非负责人账号直调 operate-log/page 读他人客户操作留痕 code=0 total=2 | TCMS 引擎实例 43359（job 2178，R57，2026-10-07 10:41:36，在役包不含本修复） |
| a106-post-api-evidence.md | 修后：同一请求受控拒绝 code=1020007001「客户操作失败，原因：没有权限」 | TCMS 引擎实例 43360（job 2179，R57，2026-10-07 10:42:45，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a106
