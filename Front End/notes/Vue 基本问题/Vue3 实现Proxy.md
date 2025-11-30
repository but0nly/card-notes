#面试题 

使用Proxy代理对象或者函数，
```js

const proxyData = new Proxy(data, {
	get(target, key){
		return Reflect.get(target, key)
	},
	set(target, key, value, reciver){
		return Reflect.set(target, key, value, reciver)
	},
	deleteProperty(target, key, reciver){
		return Reflect.deleteProperty(target, key, reciver)
	}
})

```