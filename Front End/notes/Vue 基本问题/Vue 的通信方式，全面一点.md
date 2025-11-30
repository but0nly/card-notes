#面试题 
## 场景
---

- 父子组件通信
- 兄弟组件通信
- 多层级组件通信
- 全局组件通信


## 通信方法
---
- `props` 和 `$emit`
- 自定义事件
	- Vue2是通过new Vue()的实例来创建，然后`v.event()`
	- Vue3要安装第三方库`event-emit`
- `$attributes` (Vue2是`$listeners`, Vue3移除了`$listeners`,    合并到了`$attributes`)
	- `props`和`$emit`没有包含的属性会出现在`$attributes`中
	- 可以同过`v-bind=“$attrs”`将其他没有被`props`和`$emit`包含的属性或者方法 传递给下一个组件
	- 只有一个节点会展示在HTML标签当中，可通过`inheritAttrs：false`控制不展示 
- `$parent`
	- 可以过`$parent`获取父节点的属性和方法
- `$refs`，Vue2是`$children` 
	- 通过给标签加上`ref=“refname”`属性，再通过`this.$refs.refname`获取子组件的属性和方法
- provide/inject
	- 适用于多层级通信
	- 通过上层属性`provide：{ info: "aaa" }`定义属性，然后下级通过`inject: ["info"]`获取，可以直接用在`template`中
	- 传递data中的属性时，要吧`provide`写成方法并通过`computed(()=>this.name)`包裹传递
```js
	import {computed} from "vue";

	export default {
		data:{
			name: "aaa"
		},
		provied(){
			return {
				name: computed(()=>this.name)
			}
		}
	}
```

- Vuex