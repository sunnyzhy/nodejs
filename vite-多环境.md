# vite - 多环境

## 1 新建 .env 文件

- 在项目的根目录下新建 .env 文件，跟 package.json 平级
- 环境文件格式: ```.env.[model]```
- 编译发布的时候，可以把测试环境/开发环境当作是生产环境的一种

### 1.1 新建 .env.dev(开发环境)

```.env
NODE_ENV=development
VITE_PROFILE=dev
VITE_URL=http://localhost:8080
```

### 1.2 新建 .env.prod(生产环境)

```.env
NODE_ENV=production
VITE_PROFILE=prod
VITE_URL=http://localhost:8070
```

### 1.3 新建 .env.test(测试环境)

```.env
NODE_ENV=production
VITE_PROFILE=test
VITE_URL=http://localhost:8060
```

## 2 修改 vite.config.js

```js
export default defineConfig({
  plugins: [vue()],
  base: './'
})
```

注:

- 增加配置: ```base: './'```

## 3 修改 package.json

- 编译命令的格式: ```vite build --mode [model]```
- 命令中的 ```[model]```，就是环境文件 ```.env.[model]``` 里的 model
- 修改 scripts 的 dev 为 ```vite --mode dev```
- 在 scripts 增加: ```build--dev```, ```build--test```, ```build--prod```

```json
  "scripts": {
    "dev": "vite --mode dev",
    "build": "vite build",
    "preview": "vite preview",
    "build--dev": "vite build --mode dev",
    "build--test": "vite build --mode test",
    "build--prod": "vite build --mode prod"
  }
```

## 4 演示页面

### src/App.vue

```vue
<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from './components/HelloWorld.vue'
const env = import.meta.env.VITE_URL
</script>

<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <h1>{{env}}</h1>
  <HelloWorld msg="Hello Vue 3 + Vite" />
</template>

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
