# PowerShell

### 提示禁止运行脚本

无法加载文件 D:\XXX\EditDBForSim.ps1，因为在此系统上禁止运行脚本。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies。
    + CategoryInfo          : SecurityError: (:) []，ParentContainsErrorRecordException
    + FullyQualifiedErrorId : UnauthorizedAccess


在本次会话中允许（例如PowerShell ISE中调试）：

```powershell
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
```