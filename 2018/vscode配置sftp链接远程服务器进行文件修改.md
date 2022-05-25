# vscode配置sftp链接远程服务器进行文件修改

#other

- 在vscode插件库中搜索sftp, 并安装插件
- ctrl+shift+p , 输入sftp, 选择SFTP:Config,进行配置

```json
{
    "host": "49.4.13.216”, // 远程服务器IP
    "port": 9876, // 远程服务器ssh端口
    "username": "www”, // 用户名
    "password": null, // 密码,
    "protocol": "sftp”, // 模式
    "agent": null,
    "privateKeyPath": "/Users/Kevin/.ssh/id_rsa”, // 私钥
    "passphrase": null,
    "passive": false,
    "interactiveAuth": true,
    "remotePath": "/home/www/sftp/“, // 远程服务器上文件地址
    "uploadOnSave": false,
    "syncMode": "update”,
    "watcher": { // 监听外部文件
        "files": false,
        "autoUpload": false,
        "autoDelete": false
    },
    "ignore": [ // 忽略项
        "**/.vscode/**",
        "**/.git/**",
        "**/.DS_Store"
    ]
}
```
- 常用指令

|指令|功能|
|--|--|
|SFTP Upload|上传到服务器，没有则创建，有则覆盖，多则忽略|
|SFTP Download|下载到本地，规则同上|
|SFTP Sync To Remote|同步到服务器，多则删除|
|SFTP Sync To Local|同步到本地，多则删除|







