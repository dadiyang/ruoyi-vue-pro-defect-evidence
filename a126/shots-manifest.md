# A126 证据清单（api 轨：越权类缺陷，以接口响应原文替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a126-pre-api-evidence.md | 修前：member 令牌经 app-api 提交 admin 属主待支付单 code=0 越权提交生效 | TCMS 引擎实例 43375（job 2194，R57，2026-10-07 11:11:32，在役包不含本修复） |
| a126-post-api-evidence.md | 修后：同一请求受控拒绝 1007002000「支付订单不存在」且单据仍待支付；属主经 admin-api 提交照旧成功 | TCMS 引擎实例 43380（job 2195，R57，2026-10-07 11:13:54，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a126
