#面试题 

### bind()函数的原理
- 返回一个函数, 但不执行
- 绑定 `this` 和传入参数
- 如果是箭头函数，无法改变 `this`， 只能改变参数

实现一个 `custombind` 函数

```js
Function.prototype.customBind = function(context, ...bindArgs) {
  
  let self = this;

  return function(...args) {
    const newArgs = bindArgs.concat(args);
    return self.apply(context, newArgs)
  }
}



function foo(a, b, c) {
  console.log(this, a, b, c);
}

const f = foo.customBind({x: 100}, 10, 20);

f(30) // {x: 100} 10 20 30

```