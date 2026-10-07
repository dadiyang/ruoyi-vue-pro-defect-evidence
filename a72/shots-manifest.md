# A72 证据清单（api 轨：流程卡死缺陷，以接口响应原文＋服务器日志窗口替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a72-pre-api-evidence.md | 修前：通用发起的 oa_leave 流程（无 businessKey）取消返回业务码 500「系统异常」＋服务端 NumberFormatException 堆栈，实例卡死运行中 | TCMS 引擎实例 43314（job 2142，R57，2026-10-07 09:34:01，在役包不含本修复） |
| a72-post-api-evidence.md | 修后：同一取消 code=0 成功、实例达已取消态(4)；修前遗留卡死实例亦被正常取消清净（残留=0） | TCMS 引擎实例 43315（job 2143，R57，2026-10-07 09:35:36，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a72
