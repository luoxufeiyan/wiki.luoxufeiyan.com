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

ref: 

* https://stackoverflow.com/a/1922230
* https://github.com/dotnet/wpf/issues/438