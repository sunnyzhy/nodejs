# 安装 nvm

nvm 是一个 Node.js 的版本管理工具，可以通过 nvm 安装和切换不同版本的 Node.js

## 1 下载

[nvm官网](https://github.com/coreybutler/nvm-windows/releases 'nvm')

下载 nvm-setup.zip

## 2 安装 nvm

1. 设置 nvm 安装路径 ```D:\nvm```
2. 设置 Node.js 安装路径 ```D:\nodejs```
3. 配置镜像，修改 settings.txt:
   ```txt
   root: d:\nvm
   path: d:\nodejs
   node_mirror: https://npm.taobao.org/mirrors/node/
   npm_mirror: https://npm.taobao.org/mirrors/npm/
   ```

## 3 安装 Node.js

1. 查看可下载的版本
   ```bash
   nvm list available
   ```

2. 安装，可自定义版本号
   ```bash
   nvm install 12.0.0
   ```

3. 指定版本
   ```bash
   nvm use 12.0.0
   ```

4. 查看 Node.js 版本
   ```bash
   node -v
   v12.0.0
   ```

5. 查看 npm 版本
   ```bash
   npm -v
   6.9.0
   ```
