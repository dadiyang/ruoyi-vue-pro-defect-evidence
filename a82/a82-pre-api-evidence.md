# A82 修前证据（2026-10-07 09:42:16，TCMS 引擎实例 43321 / job 2147 / 轮 57）

被测版本：master-jdk17 @ 3a6150f544 ＋在役补丁链，不含本修复。

前置：管理端建频道→建素材→群发素材（均成功，im_channel_message 已落库）。

请求（拉取频道消息）：

```
GET /admin-api/im/channel/message/pull?minId=0&size=200
```

响应（HTTP 200，业务码 500）：

```json
{"code": 500, "msg": "系统异常", "data": null}
```

服务端日志窗口（同一请求，ERROR 级堆栈）：

```
2026-10-07 09:42:16.697 [http-nio-18080-exec-6] ERROR c.i.y.f.web.core.handler.GlobalExceptionHandler:342 - [defaultExceptionHandler]
org.mybatis.spring.MyBatisSystemException:
### Error querying database.  Cause: java.lang.ClassCastException: class java.lang.String cannot be cast to class java.util.List
### The error may exist in cn/iocoder/yudao/module/im/dal/mysql/message/ImChannelMessageMapper.java (best guess)
### The error occurred while setting parameters
### SQL: SELECT ... FROM im_channel_message WHERE deleted = 0 AND (i...
```

即：查询条件 `.eq(ImChannelMessageDO::getReceiverUserIds, "")` 把 String 参数 "" 送进
字段配置的 LongListTypeHandler（按 List 处理），设参阶段直接 ClassCastException——
只要调用 pull 必炸，频道消息收取功能完全不可用。
