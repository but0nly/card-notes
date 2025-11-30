#面试题 



- componentDidMount - useEffect 第二个参数传入空数组 `[]`
	- 依赖为`[]` 的时候re-render不会重新执行effect函数
```js
useEffect(()=>{
	// 加载时调用
}, [])
```
- componentDidUpdate - useEffect 第二个参数传入依赖或者无依赖
	- 没有依赖，re-render会执行effect函数
```js
useEffect(()=>{
	// 依赖更新时调用
}, [a, b])
```
- componentWillUnMount - useEffect 返回一个函数，会在组件销毁时执行
	- 并不完全等同于willUnMount，props发生变化时，返回函数会在useEffect 更新前触发
```js


useEffect(()=>{
	return ()=>{
		// 组件销毁时调用
	}
})
```