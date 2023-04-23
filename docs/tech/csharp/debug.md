# 调试 Debug

## StackTrace

可以使用`StackTrace`类来获取当前的调用堆栈信息，所属的命名空间为`System.Diagnostics`。

```c#
System.Diagnostics.StackTrace t = new System.Diagnostics.StackTrace();
```

StackTrace类的构造函数有两个重载，一个是不带参数的，一个是带参数的。不带参数的构造函数会获取当前的调用堆栈信息，而带参数的构造函数接受 Exception 类型，会获取 Exception 的调用堆栈信息。

如果想要获取调用方法的文件名和行号，需要在构造函数中传入`true`，否则只能获取方法名。

签名如下：
```c#
public StackTrace (bool fNeedFileInfo);
```

注意 StackTrace 的执行代价很高，因为它需要获取当前的调用堆栈信息，会拖慢程序的执行速度，因此不要在生产环境中使用。

### 例子

不带参数：
```c#
void Main()
{
	System.Diagnostics.StackTrace t = new StackTrace(true);
	t.Dump(); // 获取此时的堆栈信息
}
```

带参数：
```c#
using System;

class Program {
    static void Main(string[] args) {
		try
		{
			Foo(); // 调用方法
		}
		catch (Exception ex)
		{
			Console.WriteLine("出现异常：{0}", ex.Message);

			// 获取堆栈跟踪信息
			StackTrace stackTrace = new StackTrace(ex, true);
			Console.WriteLine("堆栈跟踪信息：");
			for (int i = 0; i < stackTrace.FrameCount; i++)
			{
				Console.WriteLine("{0}.{1}({2})",
					stackTrace.GetFrame(i).GetMethod().DeclaringType.FullName,
					stackTrace.GetFrame(i).GetMethod().Name,
					stackTrace.GetFrame(i).GetFileLineNumber());
			}
		}
	}

	static void Foo()
	{
		Bar(); // 调用方法
	}

	static void Bar()
	{
		throw new Exception("Bar 方法抛出的异常");
	}
}

// Output:
// 出现异常：Bar 方法抛出的异常
// 堆栈跟踪信息：
// UserQuery+Program.Bar(33)
// UserQuery+Program.Foo(28)
// UserQuery+Program.Main(7)
```

### ref

[StackTrace Constructor (System.Diagnostics) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.diagnostics.stacktrace.-ctor?view=net-7.0#system-diagnostics-stacktrace-ctor(system-boolean))