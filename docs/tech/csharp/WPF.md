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