# package.json

## 1 scripts 语法解析

在 scripts 里定义一条命令:

```json
"echo": "echo hello"
```

***执行命令:***

```bash
> npm run echo

> hello-vue3@0.1.0 echo D:\svn\vue\hello-vue3
> echo hello

hello
```

执行 ```npm run echo``` 相当于执行 ```echo hello```

***然后执行命令:***

```bash
> npm run echo Jim

> hello-vue3@0.1.0 echo D:\svn\vue\hello-vue3
> echo hello "Jim"

hello "Jim"
```

执行 ```npm run echo Jim``` 相当于执行 ```echo hello "Jim"```

***再执行命令:***

```bash
> npm run echo --Jim

> hello-vue3@0.1.0 echo D:\svn\vue\hello-vue3
> echo hello

hello
```

执行 ```npm run echo --Jim``` , 发现 ```--Jim``` 并未生效

***再执行命令:***

```bash
> npm run echo -- Jim

> hello-vue3@0.1.0 echo D:\svn\vue\hello-vue3
> echo hello "Jim"

hello "Jim"
```

执行 ```npm run echo -- Jim``` 相当于执行 ```echo hello "Jim"```

***注: ```--```与```参数```之间有空格，```-- 参数```***
