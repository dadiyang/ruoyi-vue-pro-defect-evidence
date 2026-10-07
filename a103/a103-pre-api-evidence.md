# A103 修前证据（2026-10-07 10:38:24，TCMS 引擎实例 43357 / job 2176 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：本轮现造限制配置（id=64）→删除（DELETE /crm/customer-limit-config/delete，code=0）。

请求（查已删配置）：

```
GET /admin-api/crm/customer-limit-config/get?id=64
→ {"code": 500, "msg": "系统异常", "data": null}
```

服务器日志同刻堆栈原文：

```
java.lang.NullPointerException: Cannot invoke "cn.iocoder.yudao.module.crm.dal.dataobject.customer.CrmCustomerLimitConfigDO.getUserIds()" because "<local2>" is null
	at cn.iocoder.yudao.module.crm.controller.admin.customer.CrmCustomerLimitConfigController.getCustomerLimitConfig(CrmCustomerLimitConfigController.java:77)
```

与数据内容无关，查已删行必炸。用例断言「应受控拒绝 1020012001」失败（判 FAIL）。
