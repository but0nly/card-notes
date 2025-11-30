#面试题 

| 特性       | HTMLCollection                                         | NodeList                                                     |
| -------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| 包含内容     | 主要包含元素节点（Element）                                      | 包含任何元素节点，如元素节点、文本节点、注释节点                                     |
| “活”/ "静" | 通常是“活”的集合，集合会实时更新                                      | 可以是“活”的集合（如`clikdNodes`返回）。也可以是“静”的集合，由`querySelectorAll`返回。 |
| 常用方法     | 没有直接遍历的方法，只能通过索引访问，`[i]`或者`.item(i)`                   | 支持索引访问，`[i]`或者`.item(i)`,现大多数浏览器支持使用`forEach`访问              |
| 获取来源     | `document.getElementByClassName()`、`document.chlidren` | `document.querySelectorAll()`、`document.childNodes`          |

---
## 两者都通用遍历方法

### `for...of`
HTMLCollection和NodeList 都实现了迭代器协议。所以可以在`for...of`中直接使用

### `Array.from`
Array中的集合转换方法。第二个参数还可以接受一个可选的映射函数，让你在转换时就可以处理子项

### 拓展运算符`(...)`
将集合转换成真正的数组（Array）。然后允许你用`forEach`、`map`、`filter`等强大的数组方法。
