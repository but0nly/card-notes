#JavaScript #面试题 

# 原理
**instanceof**用来检查一个*对象*是否属于某个特定的*类*（Class）， 同时，它还考虑了继承；

用法
```js
obj instanceof Class
```

判断实例与构造函数
```js
function Rubbit(){
	//...
}

const rubbit = new Rubbit();

console.log(rubbit instanceof Rubbit) // true
```


诸如 `Array` 之类的内建 class 一起使用：
```js
const arr = [1, 2, 3];

console.log(arr instanceof Array); //true
Console.log(arr instanceof Objeact); // true
```
上面代码中，arr 隶属于 Array；也隶属于Object，因为从原型来讲Array是继承了Object；

`instanceof`会把原型继承考虑在内，此外我们还可以在静态方法`Symbol.hasInstance`中自定义逻辑

### `Symbol.hasInstance`
```js
Class Animal{
	static [Symbol.hasInstance](obj){
		if(obj.canUse) return true
	}
}

const cow = {
	canUse: true
}

console.log(cow instanceof Animal) // true
```



大多数情况下Class中是没有`Symbol.hasInstance`静态方法的，标准逻辑就是，`obj instanceof Class`就是检查`Class.prototype`是否等于`obj`原型链中的原型之一。

```js
obj.__proto__ === Class.prototype;
obj.__proto__.__proto__ === Class.prototype;
obj.__proto__.__proto__.__proto__ === Class.prototype;

// 如果对比原型链中的原型有一个是相等的，则返回true；
// 否则检查到尾端返回了false
```


下面是继承的例子
```js
Class Animal{}
Class Rubbit extend Animal{}

const rubbit = new Rubbit();

rubbit.__proto__ === Animal.prototype; // false; 一次原型并非是Class Animal
rubbit.__proto__.__proto__ === Animal.prototype; // true; 匹配！
```