# vscode 格式化插件

## 安装插件

- ESLint
- Prettier - Code formatter
- Vetur

## 配置 setting.json

打开 setting 界面，编辑 setting.json，添加以下配置:

```json
    "editor.tabSize": 2,
    "editor.formatOnSave": true, // 在保存时自动格式化
    "editor.formatOnType": false, // 在键入一行后是否自动化格式
    "editor.formatOnPaste": true, // 在粘贴时自动格式化
    "editor.wordWrap": "off", // 换行规则，off 永不换行
    "editor.detectIndentation": false, // vscode 默认是启用根据文件类型自动设置 tabSize 的值
    // 保存时按照哪个规则进行格式化
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    },
    // 开启 vscode 文件路径导航
    "breadcrumbs.enabled": true,
    // prettier 设置语句末尾不加分号
    "prettier.semi": false,
    // prettier 设置强制单引号
    "prettier.singleQuote": true,
    // prettier 设置末项不加逗号
    "prettier.trailingComma": "none",
    // 选择 vue 文件中 template 的格式化工具
    "vetur.format.defaultFormatter.html": "prettyhtml",
    
    // 显示 markdown 中英文切换时产生的特殊字符
    "editor.renderControlCharacters": true,
    
    // vetur 的自定义设置
    "vetur.format.defaultFormatterOptions": {
      "prettier": {
        "singleQuote": true, // 用单引号
        "semi": false, // 不加分号
        "trailingComma": "none" // 末项不加逗号
      }
    },
    "[vue]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    }
```
