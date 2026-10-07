# A50 修后证据（2026-10-07 09:05:25，TCMS 引擎实例 43302 / job 2130 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（refreshAccessToken 轮换刷新令牌）。令牌值经引擎脱敏。

1. 用 rt 刷新 → 成功，且返回**新的** refreshToken(rt2)：

```
POST /admin-api/system/auth/refresh-token?refreshToken=rt
→ {"code":0,"data":{"accessToken":"…","refreshToken":"rt2…"}}
```

2. 旧 rt 重放 → 受控拒绝（HTTP 200，业务码 400）：

```
POST /admin-api/system/auth/refresh-token?refreshToken=rt
→ {"code":400,"msg":"无效的刷新令牌","data":null}
```

3. 轮换后的 rt2 可继续刷新并再次轮换（正常刷新链不受影响）：

```
POST /admin-api/system/auth/refresh-token?refreshToken=rt2
→ {"code":0,"data":{"accessToken":"…","refreshToken":"rt3…"}}
```

4. 数据库核对：旧 rt 关联的有效访问令牌行数为 0（引擎 SQL 断言）。
