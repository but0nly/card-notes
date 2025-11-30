#面试题 
### apply()的功能
- 立即执行
- 改变`this`指向
- 支持原函数传参，但是只有一个参数，需要按数组索引依次传参

### 手写代码
```js
Function.prototype.customApply = function (context, args) {
  const fnKey = Symbol();

  context[fnKey] = this;

  const res = context[fnKey](...args);

  delete context[fnKey];

  return res;
}

function demo(name, age, gender) {
  console.log(this, name, age, gender);
}

demo.customApply({
  foo: 'bar'
}, ['john', 18, '男']) // { foo: 'bar', [Symbol()]: [Function: demo] } john 18 男
```

