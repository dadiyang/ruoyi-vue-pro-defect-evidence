# A91 修前证据（2026-10-07 09:59:29，TCMS 引擎实例 43331 / job 2157 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：建角色→assign-role-menu 只授按钮菜单 39（system:dept:query，不含祖先
1 系统管理/7 部门管理）→给用户绑该角色。

请求一（执行层：调按钮对应 API）：

```
GET /admin-api/system/dept/list   （普通用户 token）
→ {"code": 0, "data": [...]}        ← API 拦截层按权限标识放行
```

请求二（视图层：查自己的权限信息）：

```
GET /admin-api/system/auth/get-permission-info
→ {"code": 0, "data": {"permissions": [], "menus": []}}
```

同一授权，执行层放行、视图层为空——前端拿不到 system:dept:query，按钮入口
无法渲染，但该用户实际能调通接口（不可见却可调）。
