
#面试题 

- vue2与vue3的区别就是 distorty 变成了 Unmount



- beforeCreate （空白的实例，事件和生命周期）
- Create （Vue实例初始化完毕， inject 和 reactivity响应式）
- 是否有el 配置 最外层的入口
- 是否有template 配置 组件入口
- 有 - 模板编译进入到渲染函数； 否 - 将el最外层当作模板
- beforeMount
- 创建$el并替换"el"
- Mounted
- beforeUpdate
- Update
- beforeUnmount
- Unmounted  




## beforeCreate
---
- 创建一个空白的实例
- data、method 尚未被初始化，不可使用

## Created
---
- Vue实例初始化完毕，完成响应式绑定
- data、method 都已经初始化完毕，可以使用了
- 尚未开始渲染模板
- 这时候可以做一些与dom无关的操作


## beforeMount
---
- 编译模板，调用render生成vdom（不是真正的dom，是js层面的dom）
- 还没开始渲染DOM

## Mounted
---
- 完成DOM渲染
- 组件创建完成
- 从“创建阶段” 到了 “运行阶段”


## beforeUpdate
---
- data变化之后
- 准备更新DOM（尚未更新）


### Update
---
- data发生变化， 且DOM更新完毕
- （不要在Update里面更新data，可能会导致死循环）


## beforeUnmount
---
- 组件即将销毁（尚未销毁，可以正常使用）
- 用来解除一下全局事件，自定义事件等等


## Unmount
---
- 组件被销毁了
- 所有的子组件也被销毁了





## keep-alive组件
---
- onActivated 缓存组件被激活
- onDeactivated 缓存组件被隐藏