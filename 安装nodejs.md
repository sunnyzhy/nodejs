# 官网
https://nodejs.org/en/

# 安装
```
# cd /usr/local

# xz -d node-v9.2.0-linux-x64.tar.xz

# tar -xvf node-v9.2.0-linux-x64.tar

# mv node-v9.2.0-linux-x64 nodejs
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
v9.2.0

# npm -v
5.5.1
```

# 安装cnpm
```
# npm install -g cnpm --registry=https://registry.npm.taobao.org

# cnpm -v
cnpm@5.1.1 (/usr/local/nodejs/lib/node_modules/cnpm/lib/parse_argv.js)
npm@5.5.1 (/usr/local/nodejs/lib/node_modules/cnpm/node_modules/npm/lib/npm.js)
node@9.2.0 (/usr/local/nodejs/bin/node)
npminstall@3.2.1 (/usr/local/nodejs/lib/node_modules/cnpm/node_modules/npminstall/lib/index.js)
prefix=/usr/local/nodejs 
linux x64 3.10.0-693.5.2.el7.x86_64 
registry=http://registry.npm.taobao.org
```
