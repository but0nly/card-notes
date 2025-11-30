#面试题 


主要是通过`LRU`策略缓存 `vnode`， 最后在`render`时返回组件的`vnode`，缓存渲染过程会更新 `keep-alive` 插槽，重新再 `render` 一次，从缓存中读取之前的组件 `VNode` 实现状态缓存。