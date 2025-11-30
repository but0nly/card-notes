#面试题 


- mounted和updated都不能保证子组件全部挂载完成
- 使用$nextTick 渲染 DOM
```js

mounted(){
	this.$nextTick().then(()=>{
		// 仅在整个视图渲染完成后执行。
	})
}
```