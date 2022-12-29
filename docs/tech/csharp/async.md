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

## 返回类型

异步方法的返回类型可以是 void、Task、Task<T> 三种类型。

### Task<T> 类型

如果想要异步方法返回一个值，可以使用 Task<T> 类型，其中 T 为返回值的类型。调用方法通过task的Result属性来获取返回值。

返回值必须是T类型，或者可以隐式转换为T类型。

```c#
Task<int> value = CalculateSumAsync(1, 2);
Console.WriteLine(value.Result); 
```

### Task 类型

如果异步方法不需要返回值，但是需要检查这个方法的执行状态。可以使用 Task 类型。调用方法通过task的Wait()方法来等待异步方法执行完成。

即使异步方法中有return 语句，也不会返回值。

```c#
Task myTask = CalculateSumAsync(1, 2);
myTask.Wait();
```

### void 类型

如果只想执行一个异步方法，不需要返回值，也不需要检查执行状态，可以使用 void 类型（调用并忘记 fire and forget）。

即使异步方法中有return 语句，也不会返回值。

## 控制流

在异步方法中，遇到第一个 await 关键字之前的部分会同步执行（在调用处阻塞）。

在遇到 await 关键字时，如果返回类型为 Task 或者 Task<T>，会产生一个Task类型的对象，然后立刻返回到调用方法处，异步方法继续执行，完成 await 关键字下面的工作（可能还有其他 await 语句），然后遇到 return 语句，更新Task的属性，退出。




### ref

- [https://github.com/davidfowl/AspNetCoreDiagnosticScenarios/blob/master/AsyncGuidance.md](https://github.com/davidfowl/AspNetCoreDiagnosticScenarios/blob/master/AsyncGuidance.md)
