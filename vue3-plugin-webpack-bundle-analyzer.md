# Webpack Bundle Analyzer 插件

[webpack-bundle-analyzer官网](https://github.com/webpack-contrib/webpack-bundle-analyzer 'webpack-bundle-analyzer')

## 1 安装

```bash
npm install --save webpack-bundle-analyzer
```

## 2 使用

***代码分析报告应该在开发阶段展示，修改 ```vue.config.js```***

## 3 打开方式

### 3.1 构建时自动打开

#### 3.1.1 使用插件

1. 除端口之外，其他配置使用插件的默认值

```js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  publicPath: './',
  chainWebpack: (config) => {
    if (process.env.NODE_ENV === "development") {
      var BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin
      var plugin = new BundleAnalyzerPlugin(
        {
          analyzerMode: 'server',
          analyzerPort: 8989
        }
      )
      config
        .plugin("webpack-bundle-analyzer")
        .use(plugin)
        .end()
    }
  }
})

```

#### 3.1.2 运行

1. 运行 dev:
   ```bash
   > npm run dev
    DONE  Compiled successfully in 32392ms
    
    Webpack Bundle Analyzer is started at http://127.0.0.1:8989
    Use Ctrl+C to close it

      App running at:
      - Local:   http://localhost:${vue_port}
      - Network: unavailable
   ```
2. 浏览器会自动打开 ```http://127.0.0.1:8989```

### 3.2 使用命令行打开

#### 3.2.1 使用插件

1. 把 analyzerMode 设置为 disabled
2. 把 generateStatsFile 设置为 true
3. 端口号 analyzerPort=8989 并不会生效，需要在 package.json 的 scripts 里指定启动参数
4. openAnalyzer 是否在浏览器打开分析页面: true:自动打开;false:不打开

```js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  publicPath: './',
  chainWebpack: (config) => {
    if (process.env.NODE_ENV === "development") {
      var BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin
      var plugin = new BundleAnalyzerPlugin(
        {
          analyzerMode: 'disabled',
          generateStatsFile: true
        }
      )
      config
        .plugin("webpack-bundle-analyzer")
        .use(plugin)
        .end()
    }
  }
})
```

#### 3.2.2 修改 package.json 的 scripts

在 package.json 的 scripts 字段中新增:

```json
"report": "webpack-bundle-analyzer --port 8989 dist/stats.json"
```

#### 3.2.3 运行

1. 运行 dev:
   ```bash
   > npm run dev
   DONE  Compiled successfully in 32309ms

   Webpack Bundle Analyzer saved stats file to D:\..\${project_name}\dist\stats.json

   App running at:
   - Local:   http://localhost:${vue_port}
   - Network: unavailable
   ```
   会在当前项目结构的 dist(如果没有，会自动创建) 目录里生成一个 stats.json 文件，文件的绝对路径会输出在 terminal
2. 运行 report:
   ```bash
   > npm run report
   Webpack Bundle Analyzer is started at http://127.0.0.1:8989
   Use Ctrl+C to close it
   ```
3. 浏览器会自动打开 ```http://127.0.0.1:8989```
