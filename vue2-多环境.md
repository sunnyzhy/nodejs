# vue2-多环境

## 1 安装 cross-env 插件

```bash
npm install --global --save cross-env
```

## 2 修改 config 目录下的文件

### 2.1 dev.env.js(开发环境)

```js
'use strict'
const merge = require('webpack-merge')
const prodEnv = require('./prod.env')

module.exports = merge(prodEnv, {
  NODE_ENV: '"development"',
  PROFILE: '"dev"',
  BASE_URI: '"http://localhost:8080"'
})
```

### 2.2 prod.env.js(生产环境)

```js
'use strict'
module.exports = {
  NODE_ENV: '"production"',
  PROFILE: '"prod"',
  BASE_URI: '"http://localhost:8070"'
}
```

### 2.3 test.env.js(测试环境)

```js
'use strict'
const merge = require('webpack-merge')
const devEnv = require('./dev.env')

module.exports = merge(devEnv, {
  NODE_ENV: '"testing"',
  PROFILE: '"test"',
  BASE_URI: '"http://localhost:8060"'
})
```

### 2.4 index.js

```js
  build: {
    devEnv: require('./dev.env'),
    prodEnv: require('./prod.env'),
    testEnv: require('./test.env'),
    // Template for index.html
    index: path.resolve(__dirname, '../dist/index.html'),
    
    // ...
    
    assetsPublicPath: './',
    
    // ...
  }
```

注:

- 新增的参数: ```devEnv, prodEnv, testEnv```, 会在 ```build/webpackage.prod.conf.js``` 中使用到
- 把参数 assetsPublicPath 的值修改为 ```'./'```

## 3 修改 build 目录下的文件

### 3.1 webpack.prod.conf.js

```js
// const env = process.env.NODE_ENV === 'testing'
//   ? require('../config/test.env')
//   : require('../config/prod.env')
const env = config.build[process.env.profile + 'Env']
```

### 3.1 build.js

```js
// const spinner = ora('building for production...')
const spinner = ora('building for ' + process.env.NODE_ENV + ' of ' + process.env.profile + ' mode...')
spinner.start()
```

## 4 修改 package.json

```json
  "scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "e2e": "node test/e2e/runner.js",
    "test": "npm run unit && npm run e2e",
    "lint": "eslint --ext .js,.vue src test/unit test/e2e/specs",
    "build": "node build/build.js",
    "build--dev": "cross-env NODE_ENV=production profile=dev node build/build.js",
    "build--test": "cross-env NODE_ENV=production profile=test node build/build.js",
    "build--prod": "cross-env NODE_ENV=production profile=prod node build/build.js"
  }
```

## 5 演示页面

### src/App.vue

```vue
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{evn}}</h1>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      evn: process.env.BASE_URI
    }
  }
}
</script>

<style>
/* ... */
</style>
```

## 6 发布

### 6.1 开发环境

```bash
npm run build--dev
```

### 6.2 测试环境

```bash
npm run build--test
```

### 6.3 生产环境

```bash
npm run build--prod
```

### 6.4 安装/编译

```bash
npm install && npm run build--dev
```

## 7 运行

把生成的 dist 复制到 nginx/html 目录下。

访问 ```http://localhost/dist```，注意 vue 的 logo 下的 h1 标签值:

- 开发环境: ```http://localhost:8080```
- 测试环境: ```http://localhost:8060```
- 生产环境: ```http://localhost:8070```
