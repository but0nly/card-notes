#面试题 
### 定义
顾名思义就是*代理*的意思，通过Proxy可以去代理监听对象、数组的变化。
它允许你创建一个对象的**代理**，从而能够*拦截*和*自定义*对该对象的基本操作（例如属性查找、赋值、枚举、函数调用等）

#### 核心概念
一个`Proxy`对象由两部分组成：

1. `target`（目标对象）
	1. 被`proxy`包裹的*原始对象*。它可以是任何对象、数据甚至函数；
2. `handler`（处理对象）
	1. 一个包含*陷阱*方法的对象。这些*陷阱*定义了在代理对象执行特定的操作时触发自定义行为

#### 常见*陷阱*

| 方法                                 | 拦截的操作                         | 作用              |
| ---------------------------------- | ----------------------------- | --------------- |
| `get(target, prop, receiver)`      | 读取属性值`proxy.prop`             | 属性访问日志、默认值处理等   |
| `set(target,prop,value,receiver)`  | 设置属性值`proxy.prop = xxx`       | 数据校验            |
| `has(target,prop)`                 | 检查属性是否存在`prop in proxy`       | 自定义`in`操作符行为    |
| `deleteProperty(target,prop)`      | 删除属性`delete proxy.prop`       | 自定义属性删除行为       |
| `apply(target, thisArg, args)`     | 调用函数`proxy.prop(...args)`     | 拦截作为函数的代理对象的调用。 |
| `construct(target,args,newTarget)` | `new` 操作符`new proxy(...args)` | 拦截构造函数的调用       |
