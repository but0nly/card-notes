#面试题 

组件 data 的数据改变时，立即触发视图更新

## object.definePrototype(Vue2版本)
---

### 作用

- 监听对象的属性
- 访问和赋值的时候会触发get、set方法 

### 语法

```js
let data = {};
let name = '';
Object.definePropotype(data, 'name', {
	get(){
		console.log('--get--')
		return name
	},
	set(newValue){
		console.log('--set--')
		name = newValue;
	}
});

data.name = 'John' // --set-- 
console.log(data.name)// --get-- John
```


### 实现响应式

```js

// 触发视图更新
function updateView(params) {
  console.log('视图更新');
}


// 定义属性, 监听起来
function defineProperty(target, key, value) {
  // 深度监听
  observer(value);

  Object.defineProperty(target, key, {
    get(){
      return value;
    },
    set(newValue){
      if(value !== newValue){
        observer(newValue);

        value = newValue

        updateView()
      }
    }
  })
}


// 监听全部属性
function observer(target) {
  if(typeof target !== 'object' || target == null) {
    return target;
  }

  for (const key in target) {
    if (Object.hasOwnProperty.call(target, key)) {
      // 监听属性值
      defineProperty(target, key, target[key])
    }
  }
}

let data = {
  name: 'John',
  age: 26,
  info: {
    hobby: '篮球'
  }
};


// 开始监听
observer(data);

data.age = 18 // 视图更新
console.log(data.age);; // 18
data.name = 'Jack' // 视图更新
console.log(data.name);; // 18

// 深度监听
data.info.hobby = '足球' // 视图更新
console.log(data.info.hobby); // 足球

// 赋值对象也能够监听
data.info = { address: '广州' } // 视图更新
console.log(data.info.address); // 广州
data.info.address = '深圳' // 视图更新

// 以下两种情况不能触发更新
data.x = 'x'; // 添加新属性 不会监听到 所以有了Vue.set
delete x // 删除属性 不会监听到 所以有了Vue.delete


```


### 缺点

- 深度监听，递归到底，一次性开销过大
- 无法监听新增和删除属性
- 无法监听数组，需要特殊处理（重新定义一个原型，重写`push`、`pop`等方法）



## Proxy（Vue3.0）
---
