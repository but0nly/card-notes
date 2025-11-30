#面试题 

### bind()的功能是什么
- 改变原函数的`this`指向
- 返回一个新的函数，但不执行
- 支持原函数入参
  
### 手写代码
```js
Function.prototype.customBind = function (context, ...args1) {
	let self = this;
	return function(...args2){
		return self.apply(context, [...args1, ...args2])
	}
}

function demo(name, age, gender) {
	console.log(this, name, age, gender);
}

const demoBind = demo.customBind({
	foo: 'bar'
}, 'john');

demoBind(18, '男'); // { foo: 'bar'} john 18 男
```
  
  