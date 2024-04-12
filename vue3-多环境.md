# vue3 - 多环境

## 前言

### 环境文件

环境文件命名如下:

- ```.env```: 所有情况下都会加载
- ```.env.local```: 所有情况下都会加载，但会被 git 忽略
- ```.env.[mode]```: 只在指定模式下加载
- ```.env.[mode].local```: 只在指定模式下加载，但会被 git 忽略

**不同环境的变量可以定义在 ```.env.[mode]``` 文件中，如 ```.env.dev```、```.env.test```、```.env.prod``` 等。**

关于 ```.env``` 和 ```.env.[mode]``` 里的 key-value:

1. ```.env``` 相当于父类，```.env.[mode]``` 相当于子类，如果子类有就覆盖父类的值；如果子类没有就用父类的默认值；
2. 如果 ```.env``` 和 ```.env.[mode]``` 中有相同的 key，则后者定义的值会覆盖前者；
3. 如果在 ```.env``` 中定义了某一个 key，而在 ```.env.[mode]``` 中未定义该 key ，则默认使用前者的值；
4. **如果启动时未指定环境文件或指定的环境文件不存在，则默认加载 ```.env``` 文件。**

### 模式

默认情况下，一个 Vue CLI 项目有三个模式:

- ```development``` 模式用于 ```vue-cli-service serve```
- ```test``` 模式用于 ```vue-cli-service test:unit```
- ```production``` 模式用于 ```vue-cli-service build``` 和 ```vue-cli-service test:e2e```

你可以通过传递 ```--mode``` 选项参数为命令行覆写默认的模式。例如，如果你想要在构建命令中使用开发环境变量：

```bash
vue-cli-service build --mode development
```

***注:***

- 只有 ```NODE_ENV```，```BASE_URL``` 和以 ```VUE_APP_``` 开头的变量将通过 ```webpack.DefinePlugin``` 静态地嵌入到客户端侧的代码中
- ```BASE_URL``` 赋值无效，一般通过 ```VUE_APP_``` 进行全局变量赋值
- 在业务代码中，按以下方式访问 ```VUE_APP_``` 开头的变量:
   ```js
   console.log(process.env.VUE_APP_SECRET)
   ```

## 1 新建 .env 文件

- 在项目的根目录下新建 .env 文件，跟 package.json 平级
- 环境文件格式: ```.env.[model]```
- 编译发布的时候，可以把测试环境/开发环境当作是生产环境的一种

### 1.1 新建 .env.dev(开发环境)

```.env
NODE_ENV=development
VUE_APP_PROFILE=dev
VUE_APP_URL=http://localhost:8080
```

### 1.2 新建 .env.prod(生产环境)

```.env
NODE_ENV=production
VUE_APP_PROFILE=prod
VUE_APP_URL=http://localhost:8070
```

### 1.3 新建 .env.test(测试环境)

```.env
NODE_ENV=production
VUE_APP_PROFILE=test
VUE_APP_URL=http://localhost:8060
```

## 2 修改 vue.config.js

```js
module.exports = defineConfig({
  transpileDependencies: true,
  publicPath: './'
})
```

注:

- 增加配置: ```publicPath: './'```

## 3 修改 package.json

- 编译命令的格式: ```vue-cli-service build --mode [model]```
- 命令中的 ```[model]```，就是环境文件 ```.env.[model]``` 里的 model
- 在 scripts 增加: ```dev```, ```build--dev```, ```build--test```, ```build--prod```

```json
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint",
    "dev": "vue-cli-service serve --mode dev",
    "build--dev": "vue-cli-service build --mode dev",
    "build--test": "vue-cli-service build --mode test",
    "build--prod": "vue-cli-service build --mode prod"
  }
```

## 4 演示页面

### src/App.vue

```vue
<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <h1>{{env}}</h1>
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data () {
    return {
      env: process.env.VUE_APP_URL
    }
  }
}
</script>

<style>
/* ... */
</style>
```

## 5 发布

### 5.1 开发环境

```bash
npm run build--dev
```

### 5.2 测试环境

```bash
npm run build--test
```

### 5.3 生产环境

```bash
npm run build--prod
```

### 5.4 安装/编译

```bash
npm install && npm run build--dev
```

## 6 运行

把生成的 dist 复制到 nginx/html 目录下。

访问 ```http://localhost/dist```，注意 vue 的 logo 下的 h1 标签值:

- 开发环境: ```http://localhost:8080```
- 测试环境: ```http://localhost:8060```
- 生产环境: ```http://localhost:8070```
