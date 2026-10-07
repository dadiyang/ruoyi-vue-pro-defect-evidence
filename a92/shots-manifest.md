# A92 证据清单（api 轨：消费者崩溃类缺陷，以服务器日志堆栈与总线注入记录替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a92-pre-api-evidence.md | 修前：向 iot_device_message 总线注入已删设备消息后，场景规则消费抛 NPE（日志堆栈原文） | TCMS 引擎实例 43334（job 2160，R57，2026-10-07 10:11:55，在役包不含判空补丁）＋/home/irons/logs/yudao-server.log |
| a92-post-api-evidence.md | 修后：同一注入下 WARN 跳过、无 NPE；告警触发链等既有断言照旧 | TCMS 引擎实例 43335（job 2161，R57，2026-10-07 10:13:21，在役包含修复）＋同日志文件 |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a92
