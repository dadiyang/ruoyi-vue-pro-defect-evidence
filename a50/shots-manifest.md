# A50 证据清单（api 轨：令牌流程无界面触发面，以接口响应原文替代界面截图；令牌值经引擎脱敏）

| 文件 | 内容 | 来源 |
|---|---|---|
| a50-pre-api-evidence.md | 修前：刷新后旧 refreshToken 仍有效，二次重放照样签发新令牌 | TCMS 引擎实例 43300（job 2128，R57，2026-10-07 09:02:57，在役包临时回退轮换补丁） |
| a50-post-api-evidence.md | 修后：旧 refreshToken 重放被受控拒绝 400「无效的刷新令牌」，轮换后新令牌可继续刷新 | TCMS 引擎实例 43302（job 2130，R57，2026-10-07 09:05:25，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a50
