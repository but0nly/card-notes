#面试题 

主要通过`import`和`export`关键字来实现

### 关键特性

| 特性      | 描述                                                       |
| ------- | -------------------------------------------------------- |
| *静态化*   | 模块化的导入导出是**静态**的，是在代码编译时就能确定的依赖关系，有利于编译器优化和更早的发现错误       |
| *编译时加载* | 模块的加载在脚本执行之前完成                                           |
| *非入侵性*  | 模块内部的变量、函数都是模块私有的，不会污染全局。                                |
| *值的引用*  | `import`导入的是原始值的**引用**，当`export`导出的值在原模块中改变时，导入的值也会跟着改变。 |

### 语法
#### `export`
- 行内导出
	- ```js
	  export const name = 'John';
	  export function sayName(){
		  console.log(name);
	  }
	  ```
- 列表导出
	- ```js
	  const name = 'John'；
	  const sayName = () =>{
		  console.log(name);
	  };
	  
	  export {
		  name,
		  sayName,
	  }
	  ```
- 默认导出
	- ```js
	  export default function(){
		  console.log('I am default export.')
	  }
	  ```

#### `import`
*命名导入*
需要使用花括号`{}`，导入时名称必须与导出的名称一致（除非到导出时使用了`as`重命名）
```js
// main.js
import { name, sayHello } from './module.js';

console.log(name); // 'Alice'
sayHello(); // 'Hello'

// 导入时重命名
import { name as userName } from './module.js';
console.log(userName);
```

*默认导入*
不需要花括号
```js
// main.js
import myPerson from './module.js';

console.log(myPerson.name); // 'Bob'
```

*整体导入*
```js
// main.js
import * as Module from './module.js';

console.log(Module.name); // 'Alice'
Module.sayHello();
// 默认导出通常不包含在 `*` 中，或者需要特殊访问，但多数情况下不推荐与默认导出混用。
```


### 与**CommonJS**的区别

| 特点     | ES6模块（ESM）           | CommonJS（CJS）                          |
| ------ | -------------------- | -------------------------------------- |
| *加载时机* | 编译时静态加载              | 运行时加载                                  |
| *值/引用* | 导出值的引用               | 导出值的拷贝                                 |
| *this* | 顶层`this`为`undefined` | 顶层`this`为`module.export`               |
| *语法*   | `import`/ `export`   | `require`/ `module.export` / `exports` |
