# v-if 和 v-for 联合使用

**在同一元素上不要同时使用 ```v-for``` 和 ```v-if```。**

正确的做法：

1. 使用 ```<template>``` 标签:

```vue
<template v-if="show">
  <el-checkbox v-for="item in items" :label="item.value" :key="item.key"
    :checked="item.checked">{{item.value}}
  </el-checkbox>
</template>
```

2. 使用 ```computed``` 属性过滤出满足条件的数据:

```vue
<el-checkbox v-for="item in filterItem(items)" :label="item.value" :key="item.key"
  :checked="item.checked">{{item.value}}
</el-checkbox>

computed: {
  filterItem(items) {
    return items.filter((item, index) => {
      return !item.checked;
    });
  }
}
```
