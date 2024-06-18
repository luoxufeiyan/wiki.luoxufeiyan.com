# MessagePack

## DateTime 序列化问题

MessagePack 在序列化 DateTime 类型时，会按照[TimeStamp类型](https://github.com/msgpack/msgpack/blob/master/spec.md#timestamp-extension-type)进行处理，因此会将时间转换为UTC时间，并丢失 DateTime 中的 Kind 时区信息。

[文档中提到](https://github.com/MessagePack-CSharp/MessagePack-CSharp?tab=readme-ov-file#messagepackwriter)，可以使用 NativeDateTimeResolver 来处理这个属性，此属性使用 .NET 默认的 Int64 方式表示时间，可以保留时区信息。

例：

```csharp
[MessagePackFormatter(typeof(MessagePack.Formatters.NativeDateTimeFormatter))]
public DateTime FinishTime { get; set; }
```

Ref:

- [Add auto convert for DateTime deserialize · Issue #1474 · MessagePack-CSharp/MessagePack-CSharp](https://github.com/MessagePack-CSharp/MessagePack-CSharp/issues/1474)
- [bug(datetime): kind not deserialized properly · Issue #1167 · MessagePack-CSharp/MessagePack-CSharp](https://github.com/MessagePack-CSharp/MessagePack-CSharp/issues/1167)