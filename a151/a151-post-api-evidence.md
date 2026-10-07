# A151 修后证据（2026-10-07 11:38:29，TCMS 引擎实例 43391 / job 2205 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（closing-template-presets.json
费用借方改挂管理费用 5602 下的末级科目；upgrade SQL 向 fms_subject_template 增量补
560201 差旅费/560202 电话费/560203 房租水电费/560210 其他管理费用，已应用测试库）。

同一流程：创建账套 431 → 初始化 → 查询结账模板列表：

```
GET /admin-api/fms/closing/template/list?accountSetId=431
→ code=0，预设模板借方科目（direction=1）原文：
  daily-travel-reimbursement 报销差旅费   subjectCode "560201"（管理费用/差旅费）
  daily-telephone-expense    报销电话费   subjectCode "560202"（管理费用/电话费）
  daily-rent-utilities       支付房租水电费 subjectCode "560203"（管理费用/房租水电费）
  transfer-accrue-payroll    计提工资     subjectCode "560210"(15%) + "560209"(85%)
```

全部借方科目挂在管理费用 5602 下，经科目层级汇入 5602，即利润表"管理费用"行——
与报表模板（5601=销售费用行/5602=管理费用行/5603=财务费用行）编码体系一致。

账套初始化、科目复制（≥30 行）、财务参数、建科目不 NPE、期初余额试算平衡
（四值=66.0/差额=0/balanced=true）、不平衡录入反向等既有断言全部照旧通过。
