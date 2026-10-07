# A113 证据清单（api 轨：崩溃类缺陷，以接口响应原文＋服务器日志堆栈替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a113-pre-api-evidence.md | 修前：建产品省略 productKey 返回 code=500「系统异常」＋日志 NPE 堆栈（IotProductMapper:38 toLowerCase） | TCMS 引擎实例 43365（job 2184，R57，2026-10-07 10:52:55，在役包不含本修复）＋/home/irons/logs/yudao-server.log |
| a113-post-api-evidence.md | 修后：同一请求受控拒绝 code=400「请求参数不正确:产品 Key 不能为空」 | TCMS 引擎实例 43366（job 2185，R57，2026-10-07 10:54:09，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a113
