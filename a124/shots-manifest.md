# A124 证据清单（api 轨：脏数据写入类缺陷，以接口响应原文＋日志/DB 对账替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a124-pre-api-evidence.md | 修前：takeType=9（枚举外）创建返回 code=0 照样建成＋日志 INSERT 参数 take_type=9 | TCMS 引擎实例 43373（job 2192，R57，2026-10-07 11:06:41，在役包不含本修复）＋/home/irons/logs/yudao-server.log |
| a124-post-api-evidence.md | 修后：同一请求受控拒绝 code=400「必须在指定范围 [1, 2, 3]」；合法 ADMIN(2) 模板照旧建成 | TCMS 引擎实例 43374（job 2193，R57，2026-10-07 11:07:58，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a124
