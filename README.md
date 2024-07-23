# Profile

## npm 和 yarn

### npm 修改镜像源

```bash
# npm config set registry https://registry.npmmirror.com

# npm config get registry
https://registry.npmmirror.com

# npm config list
```

### yarn 修改镜像源

```bash
# yarn config set registry https://registry.npmmirror.com

# yarn config get registry
https://registry.npmmirror.com

# yarn config list
```

## 自动安装相关依赖（管理员身份运行）

```bash
npm install --g --production windows-build-tools
```

python 下载失败的解决办法：

```bash
npm --python_mirror=https://registry.npmmirror.com/-/binary/python/ install --global windows-build-tools
```

下载完成之后会在 ```C:\Users\用户``` 目录下生成一个 ```.windows-build-tools``` 的文件夹。点击 ```python-2.7.15.amd64.msi```，先卸载 python，再安装。
