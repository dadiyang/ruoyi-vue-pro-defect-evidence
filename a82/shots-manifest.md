# A82 证据清单（api 轨：功能不可用缺陷，以接口响应原文＋服务器日志窗口替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a82-pre-api-evidence.md | 修前：C 端拉取频道消息恒返回业务码 500「系统异常」＋服务端 ClassCastException 堆栈 | TCMS 引擎实例 43321（job 2147，R57，2026-10-07 09:42:16，在役包不含本修复） |
| a82-post-api-evidence.md | 修后：同一拉取 code=0 且推送消息内容级命中（channelId/materialId/type=125/未读态），已读转态照旧 | TCMS 引擎实例 43322（job 2148，R57，2026-10-07 09:43:38，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a82
