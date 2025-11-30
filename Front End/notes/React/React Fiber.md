#面试题 

React Fiber机制其实是一个解决方案

在 vdom 的 patch方法中有两个阶段
- `reconciliation` 阶段 - 执行diff算法，纯JS计算
- `commit` 阶段 - 将diff结果渲染DOM


可能会有性能问题，

如果组件比较复杂的话，组件更新和渲染都压力大
同时加上一些动画或者鼠标拖拽的时候，会有卡顿



解决方案 **Fiber**
- 将 `reconcilition` 阶段进行拆分，（`commit` 是渲染，无法拆分）
- 渲染的时候暂停，空闲的时候执行
- 这时候就用到了一个api `requestIdleCallback`， 在渲染空闲的时候去执行 
