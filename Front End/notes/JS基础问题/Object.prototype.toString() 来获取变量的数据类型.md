#JavaScript #面试题 

我们知道对象调用`toString()`方法会把对象输出成字符串`[object Object]`

```js
const obj = {}

console.log(obj.toString()) // [object Object]
```

但是其他的数据类型，例如undefinde、null、NaN并没有toString()方法，还有Array、Function的toString输出的格式跟Object的并不一样（这个是因为Array、Function作为Object的实例，都重写了toString方法）

以下我们用装饰器模式和转发，`call`方法去改变Object.prototype.toString()的`this`，来实现获取变量的数据类型，在内部，`toString` 的算法会检查 `this`，并返回相应的结果。

```js

const objectToString = Object.prototype.toString;

console.log(objectToString(1)); // [object Number]
console.log(objectToString('1')); // [object String]
console.log(objectToString(false)); // [object Boolean]
console.log(objectToString({})); // [object Object]
console.log(objectToString(()=>{})); // [object Function]
console.log(objectToString([]); // [object Array]
```

就这样我们就能通过`toString`来获取变量的数据类型

