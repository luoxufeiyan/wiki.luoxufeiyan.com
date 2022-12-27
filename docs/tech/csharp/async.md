# 异步

异步由异步方法和调用方法两部分组成，其中异步方法中包含至少一个的 await 关键字。

异步方法：

```c#
public static async Task<int> CalculateSumAsync(int a, int b)
{
    int sum = await Task.Run(() => GetSum(a, b)); # await 关键字，表示这里是异步操作
    return sum;
}
```

调用方法：

```c#
Task<int> tsk = CalculateSumAsync(1, 2); # 这里调用了异步方法，会立刻返回一个 Task<int> 对象，同时异步方法开始执行
```

Task<int> 是一个异步操作的占位符对象，他会在异步方法中立刻返回，然后再开始异步工作。当调用 `tsk.Result` 属性来获取结果，此时如果异步工作已经完成，会返回结果；如果未完成，会阻塞当前线程直到异步工作完成。


* 异步方法的参数不能为 out 或者 ref 关键字。
* 按照惯例，异步方法的名称以 Async 结尾。

### ref

- [https://github.com/davidfowl/AspNetCoreDiagnosticScenarios/blob/master/AsyncGuidance.md](https://github.com/davidfowl/AspNetCoreDiagnosticScenarios/blob/master/AsyncGuidance.md)
