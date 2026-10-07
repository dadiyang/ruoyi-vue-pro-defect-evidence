# A98 修前证据（2026-10-07 10:22:18，TCMS 引擎实例 43347 / job 2166 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

请求（curl 直发截断 JSON 体，Content-Type: application/json）：

```
POST /admin-api/system/notify-template/create
body: {"name": "A98截断JSON        ← 未闭合
→ {"code":500,"msg":"系统异常","data":null}
```

客户端语法错误被包成服务端"系统异常"。服务端日志同刻为
WARN GlobalExceptionHandler（HttpMessageNotReadableException: JSON parse error:
Unexpected end-of-input…），随后走 defaultExceptionHandler 兜底路径。
用例断言「应受控 400」失败（判 FAIL）。
