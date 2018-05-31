# 深拷贝
- 函数实现

```
cloneDeep(obj) {
  if (typeof obj !== 'object' || Object.keys(obj).length === 0) {
    return obj
  }
  let data = {}
  return this.recursive(obj, data)
},
recursive(obj, data = {}) {
  for (var i in obj) {
    if (typeof obj[i] == 'object' && Object.keys(obj[i].length > 0)) {
      data[i] = this.recursive(obj[i])
    } else {
      data[i] = obj[i]
    }
  }
  return data
}
```

- JSON的stringify和parse实现

```
var obj = {}

//  对象序列化为JSON字符串
var jsonString = JSON.stringify(obj)

//  把JSON字符串反序列化为对象
var jsonObject = JSON.parse(jsonString)
```
