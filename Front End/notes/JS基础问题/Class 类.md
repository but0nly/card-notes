#面试题 

```js
class User{}
console.log(typeof User) // function
```

实际上是个函数
是定义构造器和其原型方法的语法糖


### constructor
构造器

相当于 function User(){},中的函数体



### 继承

- extends
	- 继承其原型方法
- super
	- 调用父类的构造器
	- [[Front End/notes/在ES6 Class 中， super的过程中做了什么|在ES6 Class 中， super的过程中做了什么]]