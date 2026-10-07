# A98 修后证据（2026-10-07 10:24:39，TCMS 引擎实例 43348 / job 2167 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（JsonProcessingException 分支）。

同一请求（截断 JSON 体）：

```
POST /admin-api/system/notify-template/create
body: {"name": "A98截断JSON
→ {"code": 400, "msg": "请求参数格式错误:Unexpected end-of-input in VALUE_STRING", "data": null}
```

既有断言全部照旧通过：字典类型/数据 CRUD 与 DB 落库对账、同类型同值受控拒绝 1002007003、
C 端 /type 仅消费启用态、删除后软删对账等。

留痕说明：修复第一版提交 c1cbf1eb20 因 `ex.getCause()` 不自动收窄编译失败
（getOriginalMessage 找不到符号），在役分支已 revert 并重挑修正版 e4f3072701；
修前/修后判定腿均基于修正版构建，无中间态判定混入。
