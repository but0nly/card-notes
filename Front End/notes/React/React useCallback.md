#面试题 

用来缓存函数，避免重新渲染

语法
```js

const onChange = useCallback((e)=>{
	console.log(e.target.value)
}, []) // 第二个参数是空数组

```