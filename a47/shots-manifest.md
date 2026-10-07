# A47 证据清单（api 轨：无界面触发面，以接口响应原文＋服务器日志窗口替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a47-pre-api-evidence.md | 修前：伪造签名 POST 回调返回业务码 500「系统异常」＋服务端 defaultExceptionHandler 堆栈窗口 | TCMS 引擎实例 43299（job 2127，R57，2026-10-07 09:02:56，在役包临时回退验签补丁） |
| a47-post-api-evidence.md | 修后：同一请求受控拒绝回「非法请求」＋服务端仅 WARN 一行无堆栈 | TCMS 引擎实例 43301（job 2129，R57，2026-10-07 09:05:23，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a47
