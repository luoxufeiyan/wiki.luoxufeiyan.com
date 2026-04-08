# Claude code

bring your own key

```shell
# 进入项目目录
cd your-project-folder
```

Linux: 
```shell
#  Linux/Unix设置环境变量
export ANTHROPIC_AUTH_TOKEN=sk-...  # 替换为您的实际令牌
export ANTHROPIC_BASE_URL=https://www.my-own-api-endpoint.com
export API_TIMEOUT_MS=300000  # 设置为 300 秒超时
```

Windows:

```powershell
# windows PowerShell 设置环境变量
$env:ANTHROPIC_BASE_URL = "https://www.my-own-api-endpoint.com"
$env:ANTHROPIC_AUTH_TOKEN = "sk-..."
$env:API_TIMEOUT_MS = "300000"  # 设置为 300 秒超时

# windows cmd 设置环境变量
set ANTHROPIC_BASE_URL=https://www.my-own-api-endpoint.com
set ANTHROPIC_AUTH_TOKEN=sk-...
set API_TIMEOUT_MS=300000
```

```shell
# 启动 Claude Code
claude
```