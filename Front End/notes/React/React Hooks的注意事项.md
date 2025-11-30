#面试题 

- useState 初始化值，只有第一次有效（re-render无效）
- useEffect 内部不能修改state， 如果第二个参数是 `[]` 不会被触发
- useEffect 第二个值不能含有引用类型，会导致死循环
	- 因为依赖对象是用Object.is()去判断是否更新，从而去执行effect函数