# npm

## npm install

- 把依赖项安装到当前项目的 node_modules 目录中
- 不会修改 package.json
- ```npm i``` 是 ```npm install``` 的简写形式

## npm install --global

- 全局安装，把依赖项安装到 node.js 的 node_modules 目录中，但不会安装到当前项目的 node_modules 目录中
- ```npm install -g``` 是 ```npm install --global``` 的简写形式

## npm install --save

- 把依赖项安装到当前项目的 node_modules 目录中
- 在 package.json 的 dependencies 节点下添加依赖项
- ```npm install --production``` 或者注明 ```NODE_ENV=production``` 时，会自动安装依赖项到当前项目的 node_modules 目录中
- 主要用于添加生产环境的依赖
- ```npm install -S``` 是 ```npm install --save``` 的简写形式

## npm install --save-dev

- 把依赖项安装到当前项目的 node_modules 目录中
- 在 package.json 的 devDependencies 节点下添加依赖项
- ```npm install --production``` 或者注明 ```NODE_ENV=production``` 时，不会自动安装依赖项到当前项目的 node_modules 目录中
- 主要用于添加开发阶段的依赖
- ```npm install -D``` 是 ```npm install --save-dev``` 的简写形式
