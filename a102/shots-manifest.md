# A102 证据清单（api 轨：崩溃类缺陷，以接口响应原文＋服务器日志堆栈替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a102-pre-api-evidence.md | 修前：跟进分页缺 bizId 返回 code=500「系统异常」＋日志 NPE 堆栈（CrmPermissionAspect.doBefore:66） | TCMS 引擎实例 43355（job 2174，R57，2026-10-07 10:35:49，在役包不含本修复）＋/home/irons/logs/yudao-server.log |
| a102-post-api-evidence.md | 修后：同一请求受控拒绝 code=400「数据权限校验失败，原因：请求缺少参数…」 | TCMS 引擎实例 43356（job 2175，R57，2026-10-07 10:37:02，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a102
