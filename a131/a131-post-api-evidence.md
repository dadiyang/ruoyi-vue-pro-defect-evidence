# A131 修后证据（2026-10-07 11:27:45，TCMS 引擎实例 43388 / job 2202 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（TenantServiceImpl
deleteTenant/deleteTenantList 连带清理租户下用户与角色，@DataPermission(enable=false)
同款 createTenant）。

同一流程：创建租户 255（自动创建管理员用户 911 与租户管理员角色 621）→ 删除租户：

```
DELETE /admin-api/system/tenant/delete?id=255
→ {"code": 0, "data": true}
```

删除后 DB 对账（用例断言取数原文）：

```
SELECT CONCAT(id,'|',CAST(deleted AS UNSIGNED)) FROM system_users
 WHERE username='sysu451702' AND tenant_id=255
→ [["911|1"]]     ← 管理员用户随之软删
SELECT CONCAT(id,'|',CAST(deleted AS UNSIGNED)) FROM system_role
 WHERE tenant_id=255 AND code='tenant_admin'
→ [["621|1"]]     ← 租户管理员角色随之软删
```

服务器日志级联 SQL（同请求线程）：

```
UPDATE system_role SET ... deleted = 1 WHERE id IN (?) AND deleted = 0 AND tenant_id = 255
UPDATE system_user_role SET deleted = 1 WHERE ... (role_id = ?) AND tenant_id = 255
UPDATE system_role_menu SET deleted = 1 WHERE ... (role_id = ?) AND tenant_id = 255
UPDATE system_users SET ... deleted = 1 WHERE id IN (?) AND deleted = 0 AND tenant_id = 255
```

用户角色关联清零断言亦通过；多租户隔离/跨租户拒绝/同名拒绝/过期拦截等既有断言全部照旧通过。
