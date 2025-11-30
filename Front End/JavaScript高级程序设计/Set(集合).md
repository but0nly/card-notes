#JavaScript 

## Set
---
`Set`是一个特殊类型集合 - “值的集合”(没有键)，且值是唯一的，每个值只能出现一次。

- `new Set(iterable)` 创建一个`Set`集合，如果提供的是一个`iterable`对象（例如数组），将会把这个对象的所有元素复制到`Set`中。
- `set.add(value)` 添加一个值，返回`Set`本身
- `set.detele(value)` 删除一个值，如果`value`在调用时存在，则会返回`true`，反之返回`false`
- `set.has(value)` 值存在返回`true`， 反之返回`false`
- `set.clear(value)` 清空set集合
- `set.size` 返回元素的个数

```js
// 创建一个Set
const set = new Set();

set.add(1)
set.add(2)
set.add(3);

console.log(set);

```

`Set`的值是唯一的，重复使用同一个值调用`add()`方法并不会发生什么，这就是它的每个值只出现一次的原因。

```js
// Set的值都是唯一的
const set2 = new Set();

const john = {name: 'john'};
const mary = {name: 'mary'}
const pete = {name: 'pete'}

set2.add(john);
set2.add(mary);
set2.add(pete);
set2.add(john);
set2.add(mary);

console.log(set2.size);

for (const iterator of set2) {
  console.log(iterator);
}
```


## Set迭代(iterable)
---
`Set`可以使用`for...of`或者`foreach`来遍历

```js
const set = new Set([1,2,3,4]);

for(let iterator of set){
	console.log(iterator); // 1, 2, 3, 4
}

// 与forEach相同
set.forEach((value, againValue, Set)=>{
	console.log(value); // 1,2,3,4
})
```

注意一件有趣的事儿。forEach 的回调函数有三个参数：一个 value，然后是 同一个值 valueAgain，最后是目标对象。没错，同一个值在参数里出现了两次。

forEach 的回调函数有三个参数，是为了与 Map 兼容。当然，这看起来确实有些奇怪。但是这对在特定情况下轻松地用 Set 代替 Map 很有帮助，反之亦然。

Map 中用于迭代的方法在 Set 中也同样支持：

- set.keys() —— 遍历并返回一个包含所有值的可迭代对象，
- set.values() —— 与 set.keys() 作用相同，这是为了兼容 Map，
 - set.entries() —— 遍历并返回一个包含所有的实体` [value, value] `的可迭代对象，它的存在也是为了兼容 Map。