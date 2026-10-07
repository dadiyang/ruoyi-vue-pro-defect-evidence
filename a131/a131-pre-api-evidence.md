# A131 修前证据（2026-10-07 11:21:23，TCMS 引擎实例 43384 / job 2198 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：创建租户 249（createTenant 连带自动创建管理员用户 905 与租户管理员角色）；
随后删除该租户：

```
DELETE /admin-api/system/tenant/delete?id=249
→ {"code": 0, "data": true}
```

删除后 DB 对账（用例断言取数原文）：

```
SELECT CONCAT(id,'|',CAST(deleted AS UNSIGNED)) FROM system_users
 WHERE username='sysu451320' AND tenant_id=249
→ [["905|0"]]     ← 管理员用户仍活跃（deleted=0）
```

即租户行已软删，其自带的管理员用户（以及同法核对的租户管理员角色）作为活跃孤儿
数据留在库里。建卡两轮独立复现同态：租户 237/238 deleted=1 而用户 779/780、
角色 561/562 deleted=0。

可达性说明（建卡复核）：孤儿账号管理端用户列表不可见、登录被租户过滤器拦
（tenant-id=已删租户 → 1002015000 租户不存在）——现象仅 DB 级可见，无登录/安全暴露。

用例断言「删租户后其自带管理员用户应软删」失败（判 FAIL，实测 deleted=0）。
