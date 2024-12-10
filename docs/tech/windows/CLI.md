# Windows Command Line

## Setting Proxy Environment Variables in CMD and PowerShell

Set proxy environment variables (`https_proxy`, `HTTPS_PROXY`, `http_proxy`, `HTTP_PROXY`) to `http://localhost:1081` using both CMD and PowerShell.

---

### CMD Instructions

#### Temporary Settings (Session Only)
Run the following commands in a CMD terminal to set the variables for the current session:

```cmd
set https_proxy=http://localhost:1081
set HTTPS_PROXY=http://localhost:1081
set http_proxy=http://localhost:1081
set HTTP_PROXY=http://localhost:1081
```

#### Persistent Settings
To persist the changes across system restarts, use the `setx` command:

```cmd
setx https_proxy http://localhost:1081 /M
setx HTTPS_PROXY http://localhost:1081 /M
setx http_proxy http://localhost:1081 /M
setx HTTP_PROXY http://localhost:1081 /M
```

- The `/M` flag applies the settings system-wide (requires administrator privileges).
- Omit `/M` to apply the settings to the current user only.

---

### PowerShell Instructions

#### Temporary Settings (Session Only)
Run the following commands in a PowerShell terminal to set the variables for the current session:

```powershell
$env:https_proxy = "http://localhost:1081"
$env:HTTPS_PROXY = "http://localhost:1081"
$env:http_proxy = "http://localhost:1081"
$env:HTTP_PROXY = "http://localhost:1081"
```

#### Persistent Settings
To make the changes persistent, set the variables in the user or system environment:

```powershell
[System.Environment]::SetEnvironmentVariable("https_proxy", "http://localhost:1081", [System.EnvironmentVariableTarget]::User)
[System.Environment]::SetEnvironmentVariable("HTTPS_PROXY", "http://localhost:1081", [System.EnvironmentVariableTarget]::User)
[System.Environment]::SetEnvironmentVariable("http_proxy", "http://localhost:1081", [System.EnvironmentVariableTarget]::User)
[System.Environment]::SetEnvironmentVariable("HTTP_PROXY", "http://localhost:1081", [System.EnvironmentVariableTarget]::User)
```

- Replace `[System.EnvironmentVariableTarget]::User` with `[System.EnvironmentVariableTarget]::Machine` for system-wide changes (requires administrator privileges).
