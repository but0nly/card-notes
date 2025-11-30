#面试题 


- 更多的ts支持
- tree-shaking
	- 摇树，减少打包后的代码体积，引用了，但是没有用到的一些方法不会被打包的
		- 运用了esm 特点，静态
- custom render 自定义渲染，可以渲染在各个平台，不一定是在浏览器（以标签的形式）
- fragment 运用了createDocumentFragment特性， 支持多个根节点
- teleport 传送门， 可以把组件渲染到其它节点下
- composition api 