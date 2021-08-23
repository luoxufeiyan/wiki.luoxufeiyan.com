# Web

## 附件

### 在 web 项目中使用附件

在  flutter-web 项目中，使用图片（包括其他多媒体附件）需要放在 `web/assets` 目录下，并在代码中不要包括 `assets/` 前缀。


#### For example: 

文件: `./web/assets/images/1.png`

代码: 
```dart
 Image.asset(
        'images/1.png',
...
```


### 运行在固定端口

在`.vscode` 目录下添加`launch.json`文件。
```json
{   
    "version": "0.2.0",
    "configurations": [{
           "name": "Flutter",
           "request": "launch",
           "type": "dart",
           "args": ["-d", "chrome","--web-hostname", "0.0.0.0", "--web-port", "10430"],
       }
   ]}
```