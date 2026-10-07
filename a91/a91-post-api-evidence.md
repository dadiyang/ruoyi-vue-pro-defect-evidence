# A91 修后证据（2026-10-07 10:04:26，TCMS 引擎实例 43333 / job 2159 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（AuthController 禁用级联
改以全量菜单判定）。

同一授权形态（只授按钮 39 不含祖先）：

```
GET /admin-api/system/dept/list          → {"code": 0, ...}          （执行层放行，照旧）
GET /admin-api/system/auth/get-permission-info
→ {"code": 0, "data": {"permissions": ["system:dept:query"], "menus": []}}
```

视图与执行层口径一致：permissions 含 system:dept:query（按钮不进 menus 树是
buildMenuTree 的正常行为，其标识本就经 permissions 字段下发）。

既有断言全部照旧通过：完整祖先链授权时 menus 含部门管理(id7)、撤权后视图不含
标识且原授权 API 被拒 403、未授权 API 拒 403（没有该操作权限）、同名角色拒
1002002001、DB 绑定/撤销对账等。

留痕说明：实例 43332（job 2158）为修复第一版口径（改 isMenuDisabled）的验证腿，
该口径因波及菜单 simple-list 行为被放弃并 revert，最终修复为 AuthController 口径
（实例 43333 为定稿修后腿）。
