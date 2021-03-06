# 依赖注入 Dependency Injection

当A类使用B类的某些功能时，则表示A类具有B类的依赖，然而，如果在A类内部实例化B类，会导致A类与B类耦合，导致程序不易维护。

> 例如小明类内部实例化了一个手机类，当手机需要改变时还需要改造小明。

再例如：

这里 `Worker` 类依赖 `MessageWrite` 类，直接在 Worker 类里实例化了 MessageWrite 类（硬编码）。

```c#
public class Worker : BackgroundService
{
    private readonly MessageWriter _messageWriter = new MessageWriter();

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            _messageWriter.Write($"Worker running at: {DateTimeOffset.Now}");
            await Task.Delay(1000, stoppingToken);
        }
    }
}
```

导致：

* 如果 MessageWrite 的实现发生变化， Worker 类也必须修改。
* 如果 MessageWrite 有依赖项或者参数，也需要在 Worker 类里进行配置。
* 耦合太高，无法单元测试。

为了解决这个问题，需要将A类对B类的控制权抽离出来，交给一个第三方。这就是控制反转（Inversion Of Control）。
控制反转是一种思想，依赖注入（Dependency Injection）是一种实现方法。通过第三方，把B类的构造函数注入到A类里，让A类直接使用，
不需要实例化B类。

## 代码实现

定义一个 IMessageWriter 接口，在接口中实现 Write 方法。

```c#
namespace DependencyInjection.Example;

public interface IMessageWriter
{
    void Write(string message);
}
```

然后通过 MessageWriter 实现这个接口。

```C#
namespace DependencyInjection.Example;

public class MessageWriter : IMessageWriter
{
    public void Write(string message)
    {
        Console.WriteLine($"MessageWriter.Write(message: \"{message}\")");
    }
}
```

在 Main 程序中注册：

```c#
namespace DependencyInjection.Example;

class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureServices((_, services) =>
                services.AddHostedService<Worker>()
                        .AddScoped<IMessageWriter, MessageWriter>());
}
```

最后修改 Worker 类使用这个接口：

```c#
namespace DependencyInjection.Example;

public class Worker : BackgroundService
{
    private readonly IMessageWriter _messageWriter;

    public Worker(IMessageWriter messageWriter) =>
        _messageWriter = messageWriter;

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            _messageWriter.Write($"Worker running at: {DateTimeOffset.Now}");
            await Task.Delay(1000, stoppingToken);
        }
    }
}
```

## ref:
* [浅谈控制反转与依赖注入 - 胡小国的文章 - 知乎](https://zhuanlan.zhihu.com/p/33492169)
* C#代码例子：[Dependency injection in .NET | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/core/extensions/dependency-injection)
* [A quick intro to Dependency Injection: what it is, and when to use it](https://www.freecodecamp.org/news/a-quick-intro-to-dependency-injection-what-it-is-and-when-to-use-it-7578c84fa88f/)
