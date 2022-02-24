# FAQ

## 1 npm ERR! Failed at the chromedriver@x.xx.x install script.

解决方法:

```bash
# cnpm install chromedriver --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver
```

# 2 cnpm : 无法加载文件 ..\cnpm.ps1，因为在此系统上禁止运行脚本。

解决方法:

1. 运行 Windows PowerShell
2. 执行命令: 
   ```bash
   set-ExecutionPolicy RemoteSigned
   ```
