#JavaScript 

## Map
---
Map是一个带键的数据项集合，就像一个Object一样，最大的不同是它的键可以是任意类型（key）。

它的方法和属性如下：

- `new Map()` 创建一个Map
- `set(key，value)` 设置键和键值
- `get(key)` 获取匹配该键名的值， 没有则会返回undefined
- `has(key)`  判断改Map是否包含此键值，有则返回true，反之返回false
- `delete(key)`  删除匹配键的值
- `clear()`  清除全部值
- `size`  返回数据项的个数

```js
const map = new Map();

map.set(1, 'qq');
map.set("1", 'ww');
map.set(true, 'ee');

map.get(1); //qq
map.get("1"); // ww // number类型和string类型互不影响，如果是object键值的话，number类型会转换成string类型
map.get(true); // ee // 接受任意类型

const aObj = {}
map.set(aObj, 1234);

map.get(aObj) // 1234     这里要注意，用引用类型作为键的话，set和get必须是相同的对象（引用地址相同）

```

> 注意如果使用`map[key]`是不会生效的，这将会把map视为JavaScript的plain object，只能使用`set`和`get`方法


> Map是怎么比较键的？
> `Map`使用SameValueZero算法来比较键是否相等。它和严格的`===`差不多，但是区别在于`Nan`被看成是等于`Nan`的。


## Map 迭代
---
- `Map.key()` 遍历并返回一个包含所有键的可迭代对象
- `Map.value()` 遍历并返回一个包含所有键值的的可迭代对象
- `Map.entries()`遍历并返回一个包含所有实体`[key, value]`的可迭代对象。`for..of` 在默认情况下使用的就是这个。跟`Object.entries()`类似

```js
//迭代

// keys\values\entries 方法

let recipeMap = new Map([
['cucumber', 500],
['tomatoes', 350],
['onion', 50]
]);

for (const iterator of recipeMap.keys()) {
console.log(iterator); // cucumber,tomatoes,onion
}

for (const iterator of recipeMap.values()) {
console.log(iterator); //500, 350, 50
}

for (const iterator of recipeMap.entries()) {
console.log(iterator); // ['cucumber', 500],['tomatoes', 350],['onion', 50]
}
```

> 迭代的顺序和插入顺序相同，这一项不同于`Object`，`Map`保留了顺序；


## Object.entries() 从对象创建Map
---
```js
//在已有的对象来创建Map

const existObject = {
  name: 'lihua',
  age: '28'
}

const newmap = new Map(Object.entries(existObject));

for (const iterator of newmap) {
  console.log(iterator);
}

```


## Object.fromEntries() 从Map创建对象
---
```js
//已有map创建对象

const existmap = new Map();

existmap.set(1, '1');
existmap.set(2, '2');
existmap.set({property:'1'}, 'obj'); // 注意转化后的对象如果键名为对象,转化后会变成'[object Object]'


const newobj = Object.fromEntries(existmap);

console.log(newobj);
```