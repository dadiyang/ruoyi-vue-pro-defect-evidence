# A103 证据清单（api 轨：崩溃类缺陷，以接口响应原文＋服务器日志堆栈替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a103-pre-api-evidence.md | 修前：删除客户限制配置后 get 返回 code=500「系统异常」＋日志 NPE 堆栈（Controller:77） | TCMS 引擎实例 43357（job 2176，R57，2026-10-07 10:38:24，在役包不含本修复）＋/home/irons/logs/yudao-server.log |
| a103-post-api-evidence.md | 修后：同一请求受控拒绝 code=1020012001「客户限制配置不存在」 | TCMS 引擎实例 43358（job 2177，R57，2026-10-07 10:39:34，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a103
