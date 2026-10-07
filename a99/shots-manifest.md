# A99 证据清单（api 轨：崩溃类缺陷，以接口响应原文＋服务器日志堆栈替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a99-pre-api-evidence.md | 修前：未初始化账套查资产负债表 code=500「系统异常」＋日志 NPE 堆栈（validateLedgerPeriod:1414） | TCMS 引擎实例 43353（job 2172，R57，2026-10-07 10:32:38，在役包为 A99-revert 修前构建）＋/home/irons/logs/yudao-server.log |
| a99-post-api-evidence.md | 修后：同一请求受控拒绝 code=1052100005「账套尚未完成初始化」 | TCMS 引擎实例 43354（job 2173，R57，2026-10-07 10:33:53，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a99
