# 修改vscode插件安装目录

插件默认位置: "C:\Users\登录的用户名\.vscode\extensions"

步骤:

1. 把 "C:\Users\登录的用户名\.vscode" 目录下的 extensions 文件夹**剪切**到 "D:\Program Files\Microsoft VS Code" 目录里
2. 用管理员身份打开 cmd
3. 输入 mklink /D "C:\Users\Administrator\.vscode\extensions" "D:\Program Files\Microsoft VS Code\extensions"
