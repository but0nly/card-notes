#面试题 


## call
---
- 立即执行
- 改变 `this`，参数依次传入


### 思路
通过对象方法访问调用方的this去实现
```js

const obj = {x: 100, fn(){retrun this.x}}

console.log(obj.fn()) // 100
```


```js

Function.prototype.customCall = function(context, ...args){
	if(context == null) context = globalThis;
	if(typeof context !== 'object') context = new Object(context);

	const fnKey = Symbol() // 避免命名覆盖， Sybol保证唯一性
	context[fnKey] = this; // this就是调用方函数

	const res = context[fnKey](...args); // 绑定this

	delete context[fnKey] // 防止污染

	return res

}

function foo(a, b, c) {
  console.log(this, a, b, c);
}

foo.customCall({x:100}, 10, 20, 30)  // {x: 100} 10 20 30
```

## apply
---
- 立即执行
- 改变 `this`，第二个参数是数组


## 思路
跟call一样，改一下第二个参数即可



```js

Function.prototype.customApply = function(context, args){
	if(context == null) context = globalThis;
	if(typeof context !== 'object') context = new Object(context);

	const fnKey = Symbol() // 避免命名覆盖， Sybol保证唯一性
	context[fnKey] = this; // this就是调用方函数

	const res = context[fnKey](...args); // 绑定this

	delete context[fnKey] // 防止污染

	return res

}

function foo(a, b, c) {
  console.log(this, a, b, c);
}

foo.customApply({x:100}, 10, 20, 30)  // {x: 100} 10 20 30
```