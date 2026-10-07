# A96 证据清单（api 轨：静默吞类缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a96-pre-api-evidence.md | 修前：update-state 传 state=3 返回 code=0 data=true，定义状态未变 | TCMS 引擎实例 43336（job 2162，R57，2026-10-07 10:15:27，在役包不含本修复） |
| a96-post-api-evidence.md | 修后：同一请求受控拒绝 code=1009003004，定义仍处激活面 | TCMS 引擎实例 43337（job 2163，R57，2026-10-07 10:16:51，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a96
