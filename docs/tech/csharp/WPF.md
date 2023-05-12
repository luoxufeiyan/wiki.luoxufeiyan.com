# WPF


## Open directory dialog

如果不引用WinForms，可以使用下面的方法来弹出文件夹选择对话框。

使用[The Windows API Code Pack-Shell](https://www.nuget.org/packages/Microsoft.WindowsAPICodePack-Shell)来实现。

```c#
private void Button_Click(object sender, RoutedEventArgs e)
{
    var dialog = new CommonOpenFileDialog();
    dialog.IsFolderPicker = true;
    dialog.Title          = "Select the folder.";
    CommonFileDialogResult result = dialog.ShowDialog();
    if (result != CommonFileDialogResult.Ok)
    {
        MessageBox.Show("请选择正确的路径");
        return;
    }

    UserConfig.BinDirName = dialog.FileName;
}
```

### 在其他线程中更新UI

MainWindow中的UI方法如下：

```c#
public partial class MainWindow : Window
{
    /// <summary>
    /// Add a line of log to the log box.
    /// </summary>
    /// <param name="log"></param>
    public void UpdateLog(string log)
    {
        LoggerTextBox.Text += log + Environment.NewLine;
        LoggerTextBox.ScrollToEnd();
    }
}
```

如果是在其他线程中调用，需要使用`Dispatcher.Invoke`来更新UI。

```c#
public class DeployHelper
{
    public void MyBackgroundTask(string log)
    {
        if (Application.Current.MainWindow != null)
            Application.Current.MainWindow.Dispatcher.Invoke(() =>
            {
                if (Application.Current.MainWindow is MainWindow mWindow)
                {
                    mWindow.UpdateLog(log);
                }
            });
    }
}
```

ref: 

* https://stackoverflow.com/a/1922230
* https://github.com/dotnet/wpf/issues/438

## Binding

在WPF中，通过ItemSource的方式可以为控件绑定数据。

例如要在ListView中展示一个 Person 类。

首先定义一个Person类：

注意如果是在界面中展示的成员，[需要使用属性，而不是字段](https://stackoverflow.com/a/36897487)。

```c#
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    // public int Age; // 这样是错误的！
}

```

在MainWindow中定义一个Person列表，并绑定ItemSource：

```c#
List<Person> people = new List<Person>
{
    new Person { Name = "John", Age = 30 },
    new Person { Name = "Jane", Age = 25 },
    new Person { Name = "Bob", Age = 40 }
};

myListView.ItemsSource = people;

```

然后在XAML中定义ListView的显示方式：

```xml
<ListView x:Name="myListView">
    <ListView.ItemTemplate>
        <DataTemplate>
            <StackPanel>
                <TextBlock Text="{Binding Name}" />
                <TextBlock Text="{Binding Age}" />
            </StackPanel>
        </DataTemplate>
    </ListView.ItemTemplate>
</ListView>

```

ref: https://stackoverflow.com/a/36897487
