#面试题 

## setState 的两个考点
---

### setState 同步更新和异步更新

- 同步更新
	- 不在React上下文中触发
	- 例如，setTimeout、setInterval、promise.then()
	- 自定义的DOM事件
	- ajax的回调
注意：在React 18中可以异步更新

- 异步更新
	- 在React上下文中触发
	- 合成事件
	- 生命周期

### setState合并更新和不合并更新

- 合并
	- 在异步更新并且是以对象为入参的情况下
	- state相同属性会合并更新，以最后的setState为准
- 不合并
	- 同步的情况下
	- 异步更新并且是以函数为入参的情况下