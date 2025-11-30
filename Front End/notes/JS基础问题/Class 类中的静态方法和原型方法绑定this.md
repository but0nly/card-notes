#面试题 


当调用使用静态方法或原型方法的时候没有绑定this，那么this的指向会是`undefined`，不管你有没有开启`use strict`严格模式，因为Class中的严格模式是一直默认开启的。



```js

class Foo{ // 默认开启了严格模式
	static eat(){
		return this
	}

	say(){
		return this
	}
}



const foo = new Foo()；

// 原型方法
foo.say(); // Foo {};

const speak = foo.say;
speak(); // undefined


// 静态方法
foo.set(); // Foo {}

const something = foo.eat;

something(); // undefined;


```