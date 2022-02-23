# Webpack Bundle Analyzer 插件

[webpack-bundle-analyzer官网](https://github.com/webpack-contrib/webpack-bundle-analyzer 'webpack-bundle-analyzer')

## 1 安装

```bash
npm install --save webpack-bundle-analyzer
```

## 2 使用

***修改 ```webpack.dev.conf.js```***

### 2.1 引入

```js
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin
```

### 2.2 使用

- 写法 1

   ```js
   webpackConfig.plugins.push(new BundleAnalyzerPlugin({
     // ...
   }))
   ```

- 写法 2

   ```js
   var plugin = new BundleAnalyzerPlugin({
     // ...
   })
   webpackConfig.plugins.push(plugin)
   ```

- 写法 3

   ```js
   var webpackConfig = merge(baseWebpackConfig, {
   // ...
     plugins: [
       // ...
       new BundleAnalyzerPlugin({
         // ...
       })
     ]
   })
   ```

## 3 打开方式

### 3.1 构建时自动打开

#### 3.1.1 修改 BundleAnalyzerPlugin 配置

1. 使用默认配置即可，即 ```new BundleAnalyzerPlugin()```，无需配置各项参数；本示例代码列出了主要参数，仅作展示之用
2. 如果需要配置的话，只用指定端口号 analyzerPort

```js
// 运行以下命令以启动代码分析报告插件:
// npm run dev -- report
if (process.argv.indexOf('report') > 0) {
  var BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin
  var plugin = new BundleAnalyzerPlugin(
    {
       analyzerMode: 'server',
       generateStatsFile: false,
       analyzerHost: '127.0.0.1',
       analyzerPort: 8989,
       reportFilename: 'report.html',
       defaultSizes: 'parsed',
       openAnalyzer: true,
       statsFilename: 'stats.json',
       statsOptions: null,
       logLevel: 'info'
    }
  )
  webpackConfig.plugins.push(plugin)
}
```

#### 3.1.2 运行

1. 运行 dev:
   ```bash
   > npm run dev -- report
    DONE  Compiled successfully in 32392ms

    > Listening at http://localhost:${vue_port}

    Webpack Bundle Analyzer is started at http://127.0.0.1:8989
    Use Ctrl+C to close it
   ```
2. 浏览器会自动打开 ```http://127.0.0.1:8989```

### 3.2 使用命令行打开

#### 3.2.1 修改 BundleAnalyzerPlugin 配置

1. 把 analyzerMode 设置为 disabled
2. 把 generateStatsFile 设置为 true
3. 端口号 analyzerPort=8989 并不会生效，需要在 package.json 的 scripts 里指定启动参数

```js
var BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin
var plugin = new BundleAnalyzerPlugin(
  {
     analyzerMode: 'disabled',
     generateStatsFile: true,
     analyzerHost: '127.0.0.1',
     analyzerPort: 8989,
     reportFilename: 'report.html',
     defaultSizes: 'parsed',
     openAnalyzer: true,
     statsFilename: 'stats.json',
     statsOptions: null,
     logLevel: 'info'
  }
)
webpackConfig.plugins.push(plugin)
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

   > Listening at http://localhost:${vue_port}

   Webpack Bundle Analyzer saved stats file to D:\..\${project_name}\dist\stats.json
   ```
   会在当前项目结构的 dist(如果没有，会自动创建) 目录里生成一个 stats.json 文件，文件的绝对路径会输出在 terminal
2. 运行 report:
   ```bash
   > npm run report
   Webpack Bundle Analyzer is started at http://127.0.0.1:8989
   Use Ctrl+C to close it
   ```
3. 浏览器会自动打开 ```http://127.0.0.1:8989```
