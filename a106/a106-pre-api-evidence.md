# A106 修前证据（2026-10-07 10:41:36，TCMS 引擎实例 43359 / job 2178 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：admin 现造客户（ownerUserId=1）并改名产生 2 条操作留痕；另备非负责人销售账号
（crmbot1，与该客户无任何数据权限记录）登录取令牌。

请求（非负责人直调操作日志分页，bizId 指向他人客户）：

```
GET /admin-api/crm/operate-log/page?pageNo=1&pageSize=20&bizType=2&bizId=<他人客户id>
→ {"code": 0, "msg": "", "data": {"total": 2, "list": [创建客户/更新客户两条留痕原文]}}
```

即：留痕内容（谁在什么时间改了什么字段）被无权限账号完整读到——数据泄露当场坐实。
用例断言「应受控拒绝 1020007001」失败（判 FAIL）。

对照：同账号查该客户的跟进记录分页（有 @CrmPermission READ 注解的端点）受控拒绝
1020007001——防线缺失仅在 operate-log/page。
