# Event 事件

当一个事件注册多个 Handler 时，事件的触发顺序是不确定的。这取决于编译器的实现，以及 Handler 的执行时间。

```C#

public class Program
{
	public static void Main()
	{
		var eventExample = new EventExample();
		eventExample.MyEvent += EventExample_FirstHandler;
		eventExample.MyEvent += EventExample_SecondHandler;
		eventExample.MyEvent += EventExample_ThirdHandler;
		eventExample.RaiseEvent();
	}

	private static void EventExample_FirstHandler(object sender, EventArgs e)
	{
		Console.WriteLine($"First handler called, {DateTime.Now}");
	}

	private static void EventExample_SecondHandler(object sender, EventArgs e)
	{
		Console.WriteLine($"Second handler called, {DateTime.Now}");
		Thread.Sleep(5000);
	}

	private static void EventExample_ThirdHandler(object sender, EventArgs e)
	{
		Console.WriteLine($"Third handler called, {DateTime.Now}");
	}
}

public class EventExample
{
	public event EventHandler MyEvent;

	public void RaiseEvent()
	{
		MyEvent?.Invoke(this, EventArgs.Empty);
	}
}

// Output
// First handler called, 2023/4/23 13:44:10
// Second handler called, 2023/4/23 13:44:10
// Third handler called, 2023/4/23 13:44:15
```