# A70 证据清单（api 轨：错误语义缺陷，以接口响应原文＋服务器日志窗口替代界面截图）

| 文件 | 内容 | 来源 |
|---|---|---|
| a70-pre-api-evidence.md | 修前：用他人地址下单返回业务码 500「系统异常」＋服务端 defaultExceptionHandler 堆栈 | TCMS 引擎实例 43312（job 2140，R57，2026-10-07 09:30:05，在役包不含本修复） |
| a70-post-api-evidence.md | 修后：同一请求受控拒 code=1011000117「交易订单创建失败，收货地址不存在」 | TCMS 引擎实例 43313（job 2141，R57，2026-10-07 09:31:32，在役包含修复） |

已同步上证据仓：https://github.com/dadiyang/ruoyi-vue-pro-defect-evidence/tree/main/a70
