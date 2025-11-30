#JavaScript

## `Symbol.iterator`
---

我们可以通过给对象添加一个名为`Symbol.interator`的方法，让对象实现可迭代。

1. 当`for...of`循环启动时，它会调用这个方法（如果没找到，就会报错）。这个方法必须返回一个迭代器 —— 一个有`next`方法的对象
2. 从此以后`for...of` **仅用于这个被返回的对象**。
3. 当`for...of`循环希望取得下一个数值，他就会调用这个对象的`next()`方法。
4. 当`next（）`方法返回的结果格式必须是`{done: Boolean, value: any}`，当`done=true`时，表示循环结束，否则`value`就是下一个值。

```js
let range = {
		from: 1,
		to: 5
	}

// for...of首先会调这个
range[Symbol.iterator] = ()=>{
	// 它会返回一个可迭代对象
	return {
		current: this.from,
		last: this.to,
		// 当for...of循环希望取得下一个数值，它就会调用这个对象的next方法
		next: () => {
			// 它将会返回 {done:.., value :...} 格式的对象
			if(this.current <= this.last){
				return {done: false, value: this.current++}
			}else {
				return {done: true, value}
			}
		}
	}
}

// 它现在可以运行了。
for(let item of range){
	console.log(item); // 1，2，3，4，5
}
```


## `可迭代（iterable）和类数组（array-like）`
---

这两个官方术语看起来差不多，但其实大不相同。请确保你能够充分理解它们的含义，以免造成混淆。

- **Iterable** 如上所述，是实现了 `Symbol.iterator` 方法的对象。
- **Array-like** 是有索引和 `length` 属性的对象，所以它们看起来很像数组。

当我们将 JavaScript 用于编写在浏览器或任何其他环境中的实际任务时，我们可能会遇到可迭代对象或类数组对象，或两者兼有。

例如，字符串即是可迭代的（`for..of` 对它们有效），又是类数组的（它们有数值索引和 `length` 属性）。

但是一个<mark style="background: #FF5582A6;">可迭代对象也许不是类数组对象。反之亦然，类数组对象可能不可迭代。</mark>

例如，上面例子中的 `range` 是可迭代的，但并非类数组对象，因为它没有索引属性，也没有 `length` 属性。

下面这个对象则是类数组的，但是不可迭代：

```js
const range = { // 既有索引，也有length => 类数组对象
  0: 'q',
  1: 'w',
  length: 2
}


for (const item of range) { // range is not iterable
  console.log(item); 
}
```



## `Array.from`
---
有一个全局方法 [Array.from](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/from) 可以接受一个可迭代或类数组的值，并从中获取一个“真正的”数组。然后我们就可以对其调用数组方法了。

```js
let arrayLike = { 0: "Hello", 1: "World", length: 2 }; 
let arr = Array.from(arrayLike); // (*)_ alert(arr.pop()); // World（pop 方法有效）
```

在 `(*)` 行的 `Array.from` 方法接受对象，检查它是一个可迭代对象或类数组对象，然后创建一个新数组，并将该对象的所有元素复制到这个新数组。

如果是可迭代对象，也是同样：

```js
// 假设 range 来自上文的例子中 
let arr = Array.from(range); alert(arr); // 1,2,3,4,5 （数组的 toString 转化方法生效）
```


`Array.from` 的完整语法允许我们提供一个可选的“映射（mapping）”函数：

```js
Array.from(obj[, mapFn, thisArg])
```

可选的第二个参数 `mapFn` 可以是一个函数，该函数会在对象中的元素被添加到数组前，被应用于每个元素，此外 `thisArg` 允许我们为该函数设置 `this`。

例如：

```js
// 假设 range 来自上文例子中  
// 求每个数的平方 
let arr = Array.from(range, num => num * num);  alert(arr); // 1,4,9,16,25
```

技术上来讲，它和下面这段代码做的是相同的事：

```js
let str = '𝒳😂'; 
let chars = []; 
// Array.from 内部执行相同的循环 
for (let char of str) { 
	chars.push(char); 
} 
alert(chars);
```

……但 `Array.from` 精简很多。

我们甚至可以基于 `Array.from` 创建代理感知（surrogate-aware）的`slice` 方法（译注：也就是能够处理 UTF-16 扩展字符的 `slice` 方法）：

```js
function slice(str, start, end) {
  return Array.from(str).slice(start, end).join('');
}

let str = '𝒳😂𩷶';

let res = slice(str, 1, 3)
console.log(res); // 😂𩷶

// 原生方法不支持识别代理对（译注：UTF-16 扩展字符）
let res2 = str.slice(1, 3)
console.log(res2); // 乱码（两个不同 UTF-16 扩展字符碎片拼接的结果）
```


## 总结
---
可以应用 `for..of` 的对象被称为 **可迭代的**。

- 技术上来说，可迭代对象必须实现 `Symbol.iterator` 方法。
    - `obj[Symbol.iterator]()` 的结果被称为 **迭代器（iterator）**。由它处理进一步的迭代过程。
    - 一个迭代器必须有 `next()` 方法，它返回一个 `{done: Boolean, value: any}` 对象，这里 `done:true` 表明迭代结束，否则 `value` 就是下一个值。
- `Symbol.iterator` 方法会被 `for..of` 自动调用，但我们也可以直接调用它。
- <mark style="background: #FF5582A6;">内建的可迭代对象例如字符串和数组，都实现了 `Symbol.iterator`。</mark>
- 字符串迭代器能够识别代理对（surrogate pair）。（译注：代理对也就是 UTF-16 扩展字符。）

有索引属性和 `length` 属性的对象被称为 **类数组对象**。这种对象可能还具有其他属性和方法，但是没有数组的内建方法。

如果我们仔细研究一下规范 —— 就会发现大多数内建方法都假设它们需要处理的是可迭代对象或者类数组对象，而不是“真正的”数组，因为这样抽象度更高。

`Array.from(obj[, mapFn, thisArg])` 将可迭代对象或类数组对象 `obj` 转化为真正的数组 `Array`，然后我们就可以对它应用数组的方法。可选参数 `mapFn` 和 `thisArg` 允许我们将函数应用到每个元素。
