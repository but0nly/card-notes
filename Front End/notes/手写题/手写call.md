#面试题 

### call()的功能是什么
- 改变`this`指向
- 会立即调用
- 支持原函数传参，依次传参

简单思路，可以在`this`中添加函数`fn`去执行；
```js
const newThis = { x: 100, fn: function(){ console.log(this.x)}};

newThis.fn() // 100
```

*customCall*实现
```js
Function.prototype.customCall = function (context, ...args) {

  // 使用symbol保证唯一key
  const fnKey = Symbol();
  // this就是函数本身;
  context[fnKey] = this;

  // 调用后的返回结果
  const res = context[fnKey](...args);

  // 调用完成后删掉属性
  delete context[fnKey];

  //把结果再丢出去
  return res;
}

function demo(name, age, gender) {
  console.log(this, name, age, gender);
}

demo.customCall({foo: 'bar'}, 'john', 18, '男') // { foo: 'bar', fn: [Function: bound demo] } john 18 男

```