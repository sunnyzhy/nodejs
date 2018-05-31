# 安装babel-plugin-transform-react-jsx
```
cnpm install babel-plugin-syntax-jsx --save
cnpm install babel-plugin-transform-vue-jsx --save
cnpm install babel-helper-vue-jsx-merge-props --save
cnpm install babel-preset-env --save
```

# 配置.babelrc
```
{
  "presets": ["env"],
  "plugins": ["transform-vue-jsx"]
}
```

# 使用
- template
```
    <el-tree
      :data="data"
      show-checkbox
      node-key="id"
      default-expand-all
      :expand-on-click-node="false"
      :render-content="renderContent">
    </el-tree>
```

- script
```
    methods: {
      renderContent(h, { node, data, store }) {
        if(data.description === this.gatewayTypeDescription){
          return (
            <span class="custom-tree-node">
              <span>{node.label}</span>
              <span><el-tag size="mini" type="primary">标识</el-tag></span>
            </span>)
        } else {
          return (<span>{node.label}</span>)
        }
      }
    }
```
