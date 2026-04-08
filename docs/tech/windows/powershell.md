# PowerShell

### 提示禁止运行脚本

无法加载文件 D:\XXX\EditDBForSim.ps1，因为在此系统上禁止运行脚本。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies。
    + CategoryInfo          : SecurityError: (:) []，ParentContainsErrorRecordException
    + FullyQualifiedErrorId : UnauthorizedAccess


在本次会话中允许（例如PowerShell ISE中调试）：

```powershell
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
```


## 常用脚本

将目录下的多个markdown文件汇总到一起。

```powershell
Get-ChildItem -Filter *.md | Where-Object { $_.Name -ne "merged.md" } | ForEach-Object {
    $filename = $_.Name
    "# 文件名: $filename" | Out-File -FilePath "merged.md" -Append -Encoding utf8
    "`n" | Out-File -FilePath "merged.md" -Append -Encoding utf8
    Get-Content $_.FullName -Encoding utf8 | Out-File -FilePath "merged.md" -Append -Encoding utf8
    "`n`n---`n`n" | Out-File -FilePath "merged.md" -Append -Encoding utf8
}
```