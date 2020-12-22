# nodejs
[nodejs 官网](https://nodejs.org/en/ 'nodejs')

## 1. 安装 nodejs
```
# cd /usr/local

# xz -d node-v15.4.0-linux-x64.tar.xz

# tar -xvf node-v15.4.0-linux-x64.tar

# mv node-v15.4.0-linux-x64 nodejs
```

# 配置环境变量
```
# vim /etc/profile
export PATH=$PATH:/usr/local/nodejs/bin

# source /etc/profile
```

# 查看版本
```
# node -v
v15.4.0

# npm -v
7.0.15
```

# 安装cnpm
```
# npm install -g cnpm --registry=https://registry.npm.taobao.org

# cnpm -v
cnpm@6.1.1 (/usr/local/nodejs/lib/node_modules/cnpm/lib/parse_argv.js)
npm@6.14.10 (/usr/local/nodejs/lib/node_modules/cnpm/node_modules/npm/lib/npm.js)
node@15.4.0 (/usr/local/nodejs/bin/node)
npminstall@3.28.0 (/usr/local/nodejs/lib/node_modules/cnpm/node_modules/npminstall/lib/index.js)
prefix=/usr/local/nodejs 
linux x64 3.10.0-1127.19.1.el7.x86_64 
registry=https://r.npm.taobao.org
```
