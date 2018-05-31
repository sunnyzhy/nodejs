# 图片的目录结构
```
src
|_assets
|_ _custom_images
|_ _ _xx.jpg
|_ _ _yy.jpg
```

# template
```
          <template slot-scope="scope">
            <div>
              <img v-for="tag in scope.row.data"
                   :key="tag.id"
                   v-bind:src=tag.type|imgUrl
                   style="width: 26px; height: 26px;">
            </div>
          </template>
```

# script
```
  filters: {
    imgUrl(type) {
      let img = ''
      if(type === 1) {
        img = require(`@/assets/custom_images/xx.jpg`)
      } else if (type === 2) {
        img = require(`@/assets/custom_images/yy.jpg`)
      }
      return img
    }
  }
```

# 编译生成到static目录
```
dist
|_static
|_ _img
|_ _ _xx.89115c6.jpg
|_ _ _yy.960edba.jpg
```

