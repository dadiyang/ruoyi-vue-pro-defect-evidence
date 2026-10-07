# A103 修后证据（2026-10-07 10:39:34，TCMS 引擎实例 43358 / job 2177 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（控制器判空）。

同一请求（查已删配置 id=64）：

```
GET /admin-api/crm/customer-limit-config/get?id=64
→ {"code": 1020012001, "msg": "客户限制配置不存在", "data": null}
```

受控拒绝复用模块既有错误码 CUSTOMER_LIMIT_CONFIG_NOT_EXISTS(1_020_012_001)。

既有断言全部照旧通过：配置 CRUD 回显 maxCount 1→2、精确阈值边界（N+1 放行、
第 2 单钉 1020006010、上调 N+2 后放行证明拦截由配置驱动）、分页含新建行、
删除后 DB deleted=1 读回等。
