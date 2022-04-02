# vue3 - 动态表单及验证

## 效果

[动态表单及验证](./images/form.png '动态表单及验证')

## 代码

```vue
<template>
  <el-row>
    <el-form ref="formRef" :model="form" :size="formSize" label-width="120px">
      <el-form-item
        v-for="(item, index) in form.items"
        :key="index"
        :label="item.label"
        :prop="'items.' + index + '.value'"
        :rules="item.rules"
      >
        <el-input v-model="item.value"> </el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="create">Create</el-button>
        <el-button type="primary" @click="submitForm(formRef)"
          >Submit</el-button
        >
      </el-form-item>
    </el-form>
  </el-row>
</template>

<script lang="ts" setup>
import { ref, reactive } from 'vue'
import type { FormInstance } from 'element-plus'

const formRef = ref<FormInstance>()
const formSize = ref('default')
interface Item {
  label: string
  value: string
  rules?: any[]
}
interface Form {
  items: Item[]
}
const form = reactive<Form>({
  items: []
})
let num: number = 0

const create = () => {
  num++
  let item: Item = {
    label: 'name' + num,
    value: ''
  }
  if (num % 2 === 1) {
    item.rules = []
    item.rules.push({
      required: true,
      message: 'Please input ' + item.label,
      trigger: 'blur'
    })
    item.rules.push({
      min: 3,
      max: 5,
      message: 'Length should be 3 to 5',
      trigger: 'blur'
    })
  }
  form.items.push(item)
}

const submitForm = async (formEl: FormInstance | undefined) => {
  if (!formEl) return
  await formEl.validate((valid, fields) => {
    if (valid) {
      console.log('submit!')
    } else {
      console.log('error submit!', fields)
    }
  })
}
</script>
<style></style>

```

```:prop``` 绑定的语法: ```:prop="'items.' + index + '.value'"```
- ```items``` 对应 ```v-for="(item, index) in form.items"``` 里 ```form.items``` 的 ```items```
- ```index``` 对应 ```v-for="(item, index) in form.items"``` 里 ```(item, index)``` 的 ```index```
- ```value``` 既对应 ```v-for="(item, index) in form.items"``` 里 ```(item, index)``` 的 ```item.value```，也对应 ```v-model="item.value"``` 里 ```item.value``` 的 ```value```
