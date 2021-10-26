# html 引入 element-ui

以 element-ui 的 2.15.6 版本为例。

## 在线引入

```html
<!-- 引入 element-ui 的样式 -->
<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
<!-- 必须先引入 vue.js, 再引入 element-ui.js -->
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
<!-- 引入 element-ui 的组件库-->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
```

## 离线引入

需要把 vue 和 element-ui 下载到本地。

浏览地址 ```url: unpkg.com/browse/:package@:version/```, 必须以 ```/```结尾。

下载地址 ```url: unpkg.com/:package@:version/:file```:

- element.css: https://unpkg.com/element-ui@2.15.6/lib/theme-chalk/index.css

- vue.js: https://unpkg.com/vue@2.6.14/dist/vue.js

- element.js: https://unpkg.com/element-ui@2.15.6/lib/index.js

## html 引入 element-ui 的 thymeleaf 示例

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">

<head>
  <meta charset="utf-8" />
  <title>Spring Security Login</title>
  <link rel="stylesheet" href="../css/element.css">
  <script src="../js/vue.js"></script>
  <script src="../js/element.js"></script>
</head>

<body>
  <div id="app">
    <div class="login-container">
      <el-form label-position="left" label-width="0px" class="login-form" th:action="${loginUrl}" method="POST">
        <el-form-item prop="userName" style="margin-bottom: 22px">
          <el-input size="small" name="username" v-model="loginForm.userName" autoComplete="on"
                    placeholder="用户名" prefix-icon="el-icon-user">
          </el-input>
        </el-form-item>
        <el-form-item prop="password" style="margin-bottom: 22px">
          <el-input size="small" name="password" type="password" v-model="loginForm.password" autoComplete="off"
                    placeholder="密码" prefix-icon="el-icon-lock">
          </el-input>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" size="small" class="login-button" :loading="loading" native-type="submit">登录
          </el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
  <script>
    new Vue({
      el: '#app',
      data: {
        loginForm: {
          userName: 'admin',
          password: 'admin'
        },
        loading: false
      }
    })
  </script>

  <style scoped>
    .login-container {
      position: absolute;
      width: 100%;
      height: 100%;
      background-color: rgba(5, 15, 31, 1.0);
      display-outside: ruby;
    }

    .login-form {
      width: 300px;
      margin: 160px auto; /* 上下间距160px，左右自动居中*/
      background-color: rgba(32, 32, 27, 0.8); /* 透明背景色 */
      padding: 30px;
      border-radius: 10px /* 圆角 */
    }

    .login-button {
      margin-top: 20px;
      width: 100%;
      border-radius: 2px
    }
  </style>
</body>

</html>
```

## 显示 element-ui 的 icon 图标

element.css 里面引入字体样式的代码:

```css
@font-face {
	font-family:element-icons;
	src:url(fonts/element-icons.woff) format("woff"),url(fonts/element-icons.ttf) format("truetype");
	font-weight:400;
	font-display:"auto";
	font-style:normal
}
```

所以需要下载 element-icons.woff 和 element-icons.ttf:

- element-icons.woff: https://unpkg.com/element-ui@2.15.6/lib/theme-chalk/fonts/element-icons.woff

- element-icons.ttf: https://unpkg.com/element-ui@2.15.6/lib/theme-chalk/fonts/element-icons.ttf

把下载的字体样式文件放到 ```css/fonts``` 目录下即可。
