# A50 修前证据（2026-10-07 09:02:57，TCMS 引擎实例 43300 / job 2128 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，**临时回退刷新令牌轮换补丁**（即上游现尖端行为）。令牌值经引擎脱敏。

步骤与响应（HTTP 均为 200，业务码见 body）：

1. 登录签发 accessToken(at)＋refreshToken(rt)：

```
POST /admin-api/system/auth/login  →  {"code":0,"data":{"accessToken":"…","refreshToken":"…"}}
```

2. 用 rt 刷新 → 成功，签发新访问令牌：

```
POST /admin-api/system/auth/refresh-token?refreshToken=rt
→ {"code":0,"data":{"accessToken":"…","refreshToken":"…"}}
```

3. **旧 rt 二次重放 → 仍然成功**（旧刷新令牌未作废，可无限重放换新令牌）：

```
POST /admin-api/system/auth/refresh-token?refreshToken=rt
→ {"code":0,"data":{"accessToken":"…","refreshToken":"…"}}
```

即：拿到一个 refreshToken 后，无论刷新多少次，该 refreshToken 始终有效；
已签发的旧访问令牌除主动 logout 外无法吊销，泄露的 refreshToken 可被无限期重放。
