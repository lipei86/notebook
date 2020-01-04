# 在vscode中使用jupyter
需要安装python插件，Python插件里带有jupyter。

## 连接远程jupyter server
在命令行中启动jupyter server后，会提示server的地址。
在vscode中通过快捷键 `shift + ctrl + p` 打开命令面板，输入 Python: Specify Jupyter server URI`，在提示框中输入命令行中的server地址。
例如：http://localhost:8889/?token=d3dec7c423b86de87041e4c0c8d8bcb9b2a8f113472ff254