#面试题 

- h函数     接受一个tag，属性、子节点
	- 返回 vnode 数据结构
- patch 函数
	- 怎么把一个vnode节点渲染到dom节点中
	- 新的vnode 更新到 旧的vnode 结构中






## diff

- 只比较同层级，不跨级比较
- tag不同，直接删除重建
- 使用key来标记子节点
- tag 和 key都相同 认为是相同节点，不再深度比较
	- 否则通过diff算法去比较vdom