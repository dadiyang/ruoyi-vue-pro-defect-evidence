# A112 修前证据（2026-10-07 10:49:49，TCMS 引擎实例 43363 / job 2182 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：创建跟进记录但省略非必填的 contactIds/businessIds：

```
POST /admin-api/crm/follow-up-record/create
{"bizType":2,"bizId":<客户id>,"type":3,"content":"R15跟进18-NULL...","nextTime":...}
→ {"code": 0, "data": 366}
```

DB 对账（create 侧）：`crm_follow_up_record` id=366 → contact_ids=NULL、business_ids=NULL。

请求（跟进记录分页）：

```
GET /admin-api/crm/follow-up-record/page?pageNo=1&pageSize=50&bizType=2&bizId=<客户id>
→ {"code": 500, "msg": "系统异常", "data": null}
```

服务器日志同刻堆栈原文：

```
java.lang.NullPointerException: Cannot invoke "java.util.List.stream()" because the return value of "cn.iocoder.yudao.module.crm.dal.dataobject.followup.CrmFollowUpRecordDO.getContactIds()" is null
	at cn.iocoder.yudao.module.crm.controller.admin.followup.CrmFollowUpRecordController.lambda$getFollowUpRecordPage$0(CrmFollowUpRecordController.java:95)
```

一行 NULL 编号记录使整个载体跟进分面对所有查看者崩溃。对照腿：创建时传空数组的记录
分页正常（差异只在 NULL 与空数组）。用例断言「分页面应正常」失败（判 FAIL）。
