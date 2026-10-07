# A111 证据清单（api 轨：崩溃类缺陷，以接口响应原文＋服务器日志堆栈替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a111-pre-api-evidence.md | 修前：通用发起无 businessKey 请假流程后管理员取消返回 code=500「系统异常」＋日志 NumberFormatException 堆栈（HrmAttendanceLeaveStatusListener:29）＋实例仍运行中（取消被回滚） | TCMS 引擎实例 43361（job 2180，R57，2026-10-07 10:46:23，在役包不含本修复）＋/home/irons/logs/yudao-server.log＋ACT 表对账 |
| a111-post-api-evidence.md | 修后：同一请求 code=0 取消成功实例达终态 4＋日志 WARN 跳过回写 | TCMS 引擎实例 43362（job 2181，R57，2026-10-07 10:47:54，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a111
