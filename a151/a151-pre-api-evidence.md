# A151 修前证据（2026-10-07 11:35:47，TCMS 引擎实例 43390 / job 2204 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：创建账套 430 → PUT /fms/config/account-set/initialize（初始化从科目模板复制科目、
按 closing-template-presets.json 预置结账模板）。随后查询该账套结账模板列表：

```
GET /admin-api/fms/closing/template/list?accountSetId=430
→ code=0，预设模板借方科目（direction=1）原文：
  daily-travel-reimbursement 报销差旅费   subjectCode "560107"
  daily-telephone-expense    报销电话费   subjectCode "560101"
  daily-rent-utilities       支付房租水电费 subjectCode "560102"
  transfer-accrue-payroll    计提工资     subjectCode "560110"(15%) + "560209"(85%)
```

而报表模板（fms_report_template，git 152036a7ab 按 2013 小企业会计准则绑码）把
5601 绑定为利润表"销售费用"行（子项 560115 商品维修费/560116 广告和业务宣传费）、
5602 绑定为"管理费用"行、5603 绑定为"财务费用"行。上述 5601xx 借方科目经科目层级
汇入 5601，即差旅费/电话费/房租水电/计提工资 15% 部分静默流入销售费用行而非管理费用行。

互斥性实证（建卡阶段，引擎实例 43267-43269）：若科目目录中不含 560107 等码
（从科目模板删除后初始化），账套初始化被受控拒绝 1052105025（预设所需科目码缺失）
——单一科目目录无法同时语义满足两套编码体系。

用例断言"结账预设费用借方应属管理费用 5602 一类科目"失败（判 FAIL，实测 560107）。
