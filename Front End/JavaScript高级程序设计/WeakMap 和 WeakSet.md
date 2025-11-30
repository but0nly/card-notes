#JavaScript 

## WeakMap（弱的映射）
---
`WeakMap`和`Map`的第一个不同点就是，WeakMap的键只能是对象，不是是原始值。

第二个不同点：如果键在其他地方没有引用（会被垃圾回收机制回收），那么这个键会被从内存自动清除。

```js
const visitMap = new WeakMap();

function countUser(user){
	const count = visitMap.get(user) || 0;
	visitMap.set(user, count + 1);
}

  
function getUserVisitCount(user) {
	return visitMap.get(user);
}

let john = { name: 'john'}

countUser(john);

// 查询该用户访问次数
console.log(getUserVisitCount(john));

//用户离开后
john = null

// 内存被回收, weakMap中的键值也会删除
//一旦通过其他方式无法访问这些对象，垃圾回收便会将这些对象与其关联值一同删除。
console.log(getUserVisitCount(john));
```

第三个不同点：`WeakMap`无法使用迭代方法，因此不能拿到全部键。
`WeakMap` 只有以下的方法：

- `weakMap.get(key)`
- `weakMap.set(key, value)`
- `weakMap.delete(key)`
- `weakMap.has(key)`


为什么会有这种限制呢？这是技术的原因。如果一个对象丢失了其它所有引用（就像上面示例中的 `john`），那么它就会被垃圾回收机制自动回收。但是在从技术的角度并不能准确知道 **何时会被回收**。

这些都是由 JavaScript 引擎决定的。JavaScript 引擎可能会选择立即执行内存清理，如果现在正在发生很多删除操作，那么 JavaScript 引擎可能就会选择等一等，稍后再进行内存清理。所以`WeakMap`当前的元素是未知的，JavaScript引擎可能清理了其中垃圾，也可能没有清理，因此不支持访问`WeakMap`的所有键的方法。




## WeakSet（弱集合）
---
`WeakSet`和`WeakMap`的表现类似
- 只能存储对象，所以键不能是原始值，必须是对象。
- 对象只有在其它地方能够被引用的时候，才能留在`WeakSet`中。
- 也不支持访问`WeakSet`的所有键。

```js

const weakSet = new WeakSet()；

let john = { name: 'john'};
let pete = { name: 'pete'};
let mary = { name: 'mary'};

weakSet.add(john);
weakSet.add(pete);
weakSet.add(mary);

console.log(weakSet.has(john)) // true;
console.log(weakSet.has(mary)) // false;

john = null;

//weakSet 将会自动清理值john（即自动清除其中已失效的值 john）

```




## 总结
---
`WeakMap` 是类似于 `Map` 的集合，它仅允许对象作为键，并且一旦通过其他方式无法访问这些对象，垃圾回收便会将这些对象与其关联值一同删除。

`WeakSet` 是类似于 `Set` 的集合，它仅存储对象，并且一旦通过其他方式无法访问这些对象，垃圾回收便会将这些对象删除。

它们的主要优点是它们对对象是弱引用，所以被它们引用的对象很容易地被垃圾收集器移除。

这是以不支持 `clear`、`size`、`keys`、`values` 等作为代价换来的……

`WeakMap` 和 `WeakSet` 被用作“主要”对象存储之外的“辅助”数据结构。一旦将对象从主存储器中删除，如果该对象仅被用作 `WeakMap` 或 `WeakSet` 的键，那么该对象将被自动清除。