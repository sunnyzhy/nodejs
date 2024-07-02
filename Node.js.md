# Node.js
[Node.js 官网](https://nodejs.org/en/ 'Node.js')

## 1. 安装 Node.js
```bash
# cd /usr/local

# xz -d node-v15.4.0-linux-x64.tar.xz

# tar -xvf node-v15.4.0-linux-x64.tar

# mv node-v15.4.0-linux-x64 nodejs
```

## 2. 配置环境变量
```bash
# vim /etc/profile
export PATH=$PATH:/usr/local/nodejs/bin

# source /etc/profile
```

## 3. 查看版本
```bash
# node -v
v15.4.0

# npm -v
7.0.15
```

### 4 查看 npm 默认的仓库地址
```bash
# npm config get registry
https://registry.npmjs.org/
```

查看 npm 的安装目录:

```bash
# npm -g bin
d:\nodejs
```

## 5. 安装 cnpm
### 5.1 安装方式一
```bash
# npm install -g cnpm --registry=https://registry.npmmirror.com

# cnpm -v
cnpm@6.1.1 (/usr/local/nodejs/lib/node_modules/cnpm/lib/parse_argv.js)
npm@6.14.10 (/usr/local/nodejs/lib/node_modules/cnpm/node_modules/npm/lib/npm.js)
node@15.4.0 (/usr/local/nodejs/bin/node)
npminstall@3.28.0 (/usr/local/nodejs/lib/node_modules/cnpm/node_modules/npminstall/lib/index.js)
prefix=/usr/local/nodejs 
linux x64 3.10.0-1127.19.1.el7.x86_64 
registry=https://r.npm.taobao.org
```

安装完成之后，可以用 cnpm 替换 npm:

- npm 命令为: ```npm install --save axios```
- cnpm 命令为: ```cnpm install --save axios```

### 5.2 安装方式二
```bash
# npm config set registry https://registry.npmmirror.com

npm config get registry
https://registry.npmmirror.com
```

设置完成之后，依然用 ```npm``` 命令，但是实际是从淘宝的国内服务器下载。

## 6. 安装 yarn

```bash
npm install -g yarn
```
