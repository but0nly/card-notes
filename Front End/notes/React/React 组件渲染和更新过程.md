#面试题 
### 渲染过程
- 实例 `props state`
- 通过 `render` 函数把 *JS* 模拟的 **DOM** 结构通过 `createElement` 转换成 `vnode`
- 通过 `patch` 函数渲染到 **DOM** 上 （patch(elm, vnode) 或者 patch(vnode, newvnode)）



### 更新过程
- setState() -> 保存组件放到dirtyComponents组件中（可能有子组件）
- 把dirtyComponents中的组件通过render函数，转换成 `vnode`
- 再通过patch(vnode, newvnode)更新组件