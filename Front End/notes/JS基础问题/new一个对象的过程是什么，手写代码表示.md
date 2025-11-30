#面试题 

用Function写一个构造函数
```js
function Foo(name, age){
	this.name = name
	this.age = age
}

// 在构造函数的原型写一个getName方法，new过程中空对象会继承构造函数的原型
Foo.prototype.getName = function(){ 
	console.log(this.name)
}

const f = new Foo("杰克"，26);

console.log(f)// {name: "杰克"，age: 26} // 返回一个obj
console.log(f.getName()) // 杰克 // 继承了Foo的原型，包含getName方法

```

1. 创建一个空对象（`obj`），继承构造函数的原型
2. 执行构造函数（把空对象（`obj`）变成`this`）
3. 返回`obj`


### 手写一个customNew

```js
// 我们先创建一个构造函数, 跟上面的构造函数是一样的，只不过我们用了ES6 class的语法糖
class Foo{
	constructor(name, age){
		this.name = name;
		this.age = age;
	}
	getName(){
		console.log(this.name)
	}
}


// 然后我们不能用new 运算符去创建实例
// const f = new Foo("杰克"，26)；



//我们定义一个customNew方法去实现new该做的事
function customNew(constructor, ...agurment){
	// 创建一个空对象，继承构造函数的原型
	let obj = Object.create(constructor.prototype);

	// 执行构造函数，把obj变成this，我们通过装饰器转发并传入剩下参数
	constructor.apply(obj, ...agurment);
	
	//最后返回obj
	reture obj
}


const f = customNew(Foo, "杰克"， 26)；

console.log(f)// {name: "杰克"，age: 26} // 返回一个obj
console.log(f.getName()) // 杰克 // 继承了Foo的原型，包含getName方法


```

实现成功，跟上文的new 运算符效果一致。