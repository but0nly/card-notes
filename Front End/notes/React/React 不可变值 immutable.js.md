#面试题 

```js
let map1 = Immutable.Map({'a': 1, 'b': 2, 'c': 3});
let map2 = map1.set('b', 50);

console.log(map1.get('b')) // 2
console.log(map2.get('b')) // 50
```