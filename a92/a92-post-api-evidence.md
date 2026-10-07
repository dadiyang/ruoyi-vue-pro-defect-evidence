# A92 修后证据（2026-10-07 10:13:21，TCMS 引擎实例 43335 / job 2161 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链＋本修复（executeSceneRuleByDevice 判空）。

同一注入步骤（本轮第二设备 id=384，建后立即删，XADD 同款消息）：

```
2026-10-07 10:13:18.416 [SimpleAsyncTaskExecutor-3] WARN  c.i.y.m.i.s.rule.scene.IotSceneRuleServiceImpl:205 - [executeSceneRuleByDevice][设备(384) 不存在]
```

- 场景规则消费组 WARN 跳过并正常 ack，日志无 NPE（活动日志中 NPE 签名仅存修前 10:11:52 一条）；
- 三个消费组 pending 均清零（用例 finally 对注入消息 XACK＋XDEL 成对清场，未触发重投阈值）；
- 既有断言全部照旧通过：场景规则属性触发→告警配置命中→告警记录生成（快照对账）、
  站内信送达与渲染参数对账、处理闭环（processStatus+备注）、不满足条件不新增记录等。
