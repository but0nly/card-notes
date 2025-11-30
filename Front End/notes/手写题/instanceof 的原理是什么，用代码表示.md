#面试题 

- 例如 `f instanceof Foo`
- 顺着 `f`的隐式数据`__proto__` 向上查找（原型链）
- 是否找到 `Foo.prototype`


实现 `myInstanceof`

```js

function myInstanceof(instance, origin){
	 const type = typeof instance
	 if(type !== 'object' && type !== 'function'){
	 // instance 无法判断基本类型
		 return false
	 }
	
	let tempInstance = instance;
	// 使用while顺着__proto__向上查找
	while(tempInstance){
		//是否找到匹配的原型对象
		if(tempInstance.__proto__ === origin.prototype){
			return true
		}

		// 找不到继续往上级查找
		tempInstance = tempInstance.__proto__
		
	}

	// 直到tempInstance为null返回fasle
	return false
	
}


class Foo{};

const f = new Foo();

const res = myInstanceOf(f, Foo);

console.log(res); // true

```