# A92 修前证据（2026-10-07 10:11:55，TCMS 引擎实例 43334 / job 2160 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

载体步骤（IOT-12 v4 新增腿）：建产品/物模型/设备链→另建第二设备（id=382）并立即删除→
用 redis-cli 向总线直注该已删设备的消息（记录字段与生产消息一致）：

```
redis-cli XADD iot_device_message '*' payload \
  '{"id":"rega92382","deviceId":382,"tenantId":1,"method":"thing.property.post","params":{"temperature":30}}'
```

约 20ms 后场景规则消费组炸出 NPE（服务器日志原文）：

```
2026-10-07 10:11:52.049 [SimpleAsyncTaskExecutor-3] ERROR o.s.d.r.s.DefaultStreamMessageListenerContainer$LoggingErrorHandler:343 - Unexpected error occurred in scheduled task
java.lang.NullPointerException: Cannot invoke "cn.iocoder.yudao.module.iot.dal.dataobject.device.IotDeviceDO.getTenantId()" because "<local2>" is null
	at cn.iocoder.yudao.module.iot.service.rule.scene.IotSceneRuleServiceImpl.executeSceneRuleByDevice(IotSceneRuleServiceImpl.java:203)
```

NPE 使消息不 ack、留在消费组 pending 列表；框架重投作业 RedisPendingMessageResendJob
每 1 分钟扫描、超 5 分钟未 ack 的消息重新 XADD 回总线→再次炸→无限循环。
历史日志（yudao-server.log.2026-10-02.*）同款 NPE 计数 677，即该循环的真实发生形态。
用例断言「日志应出现 WARN 跳过且不得出现 NPE」失败（判 FAIL）。
