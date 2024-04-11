# 生成 uuid

UUID 版本：

- v1: 根据时间和节点 ID（通常是 MAC 地址）生成 UUID；
- v2: 根据标识符（通常是组或用户 ID）、时间和节点 ID 生成 UUID；
- v3 和 v5: 通过散列 (hashing) 命名空间 (namespace) 标识符和名称生成 UUID；
- v4: 使用随机性或伪随机性生成 UUID。

## Nodejs

安装 node-uuid：

```bash
npm install node-uuid
```

示例：

```javascript
import uuid from 'node-uuid'; // 或者 const uuidv1 = require('uuid/v1');

console.log(uuid.v1());
console.log(uuid.v4());
```

## TypeScript

安装 uuid：

```bash
npm install uuid
```

```typescript
import { v1 as uuid } from 'uuid'; # import { v4 as uuid } from 'uuid';

const uid: string = uuid();
console.log(uid);
```

## JavaScript

```uuid/v1``` 示例：

```javascript
function uuid(timestamp) {
  if (typeof crypto === 'object') {
    if (typeof crypto.randomUUID === 'function') {
      return crypto.randomUUID();
    }
    if (typeof crypto.getRandomValues === 'function' && typeof Uint8Array === 'function') {
      const callback = c => {
        const num = Number(c);
        return (num ^ (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (num / 4)))).toString(16);
      };
      return ([1e7] + -1e3 + -4e3 + -8e3 + -1e11).replace(/[018]/g, callback);
    }
  }

  let perforNow = (typeof performance !== 'undefined' && performance.now && performance.now() * 1000) || 0;
  return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, c => {
    let random = Math.random() * 16;
    if (timestamp > 0) {
      random = (timestamp + random) % 16 | 0;
      timestamp = Math.floor(timestamp / 16);
    } else {
      random = (perforNow + random) % 16 | 0;
      perforNow = Math.floor(perforNow / 16);
    }
    return (c === 'x' ? random : (random & 0x3) | 0x8).toString(16);
  });
}

const timestamp = new Date().getTime();
const uid = uuid(timestamp);
console.log(uid);
```
