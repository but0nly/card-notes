#面试题 


- 来源不清晰（多个Mixin合并下）
- 命名覆盖（多个Mixin合并，相同的命名被覆盖）



### 使用 Vue slots 来解决
```js

const Foo = {
	data(){
		return {
			x: 0,
			y: 0
		}
	}
	template:`<div><slot :x="x" :y="y" ></slot></div>`
}


const Bar = {
	component: {
		Foo
	},
	template: `
		<div>
			<template v-slot="{x, y}"></template>
		</div>
	`
}


```