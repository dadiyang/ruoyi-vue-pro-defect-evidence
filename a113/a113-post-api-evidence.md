# A113 修后证据（2026-10-07 10:54:09，TCMS 引擎实例 43366 / job 2185 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（IotProductSaveReqVO 补
@NotEmpty(message = "产品 Key 不能为空")，Schema requiredMode 同步改 REQUIRED）。

同一请求（建产品省略 productKey）：

```
POST /admin-api/iot/product/create（同上省略 productKey）
→ {"code": 400, "msg": "请求参数不正确:产品 Key 不能为空", "data": null}
```

受控拒绝走全局参数校验通道（MethodArgumentNotValidException→400），
与该 VO 其余必填字段（产品名称/分类/协议类型等）同款防线。

既有断言全部照旧通过：显式传 Key 创建成功、productSecret 自动生成、
同 Key 重复创建钉 1050001001、更新不改 productKey/secret、删除后 deleted=1 读回等。
