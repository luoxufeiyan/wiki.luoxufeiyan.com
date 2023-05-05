## Interactive Programming 交互式编程

将 C# 安装至 jupyter，实现交互式编程：[Using .NET notebooks with Jupyter Notebook / JupyterLab](https://github.com/dotnet/interactive/blob/main/docs/NotebookswithJupyter.md)。

或者也可以使用LINQPad或者[C# REPL](https://github.com/waf/CSharpRepl)来实现类似功能。

### Import package

import from NuGet: `#r "nuget:<package name>,<package version>"`

can be found in NuGet package page, under **Script & Interactive** tab.

eg:

```c#
#r "nuget: morelinq, 3.3.2"
using MoreLinq;
```

ref: https://devblogs.microsoft.com/dotnet/net-core-with-juypter-notebooks-is-here-preview-1/