# A131 证据清单（api 轨：DB 级孤儿数据类缺陷，以接口响应原文＋DB 对账＋日志 SQL 替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a131-pre-api-evidence.md | 修前：删除租户 code=0 但其自带管理员用户 deleted=0、租户管理员角色 deleted=0 活跃残留 | TCMS 引擎实例 43384（job 2198，R57，2026-10-07 11:21:23，在役包不含本修复） |
| a131-post-api-evidence.md | 修后：同一流程用户 deleted=1、角色 deleted=1，日志见级联 UPDATE 软删 SQL 与关联清理 | TCMS 引擎实例 43388（job 2202，R57，2026-10-07 11:27:45，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a131
