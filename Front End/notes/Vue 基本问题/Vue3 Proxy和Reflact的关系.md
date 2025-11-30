#面试题 


```js

const parent = {
  get value() {
    return 'farmerLZJ';
  },
};

const proxy = new Proxy(parent, {
  // get方法中target表示原对象 key表示访问的属性名
  get(target, key, receiver) {
    console.log(receiver === proxy); // 这里的代理对象已经被修改了，指向的是obj
    return target[key];
  },
});

const obj = {
  name: 'demoName',
};

// 设置obj继承parent的代理对象proxy
Object.setPrototypeOf(obj, proxy);

// log: false
obj.value

```


- Proxy 中的 get，set方法的第三个参数receiver形参，代表了代理对象本身或者继承代理对象的对象
- Reflact 中的receiver实参，表示修改执行原始操作时的this指向



### 作用
为了触发代理对象的劫持时保证this上下文指向