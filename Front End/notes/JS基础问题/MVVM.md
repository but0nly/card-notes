#面试题 

MVVM分别是Model（数据层）、View（视图层）、View-Model（视图模型），View通过View-Model的Listeners将事件绑定到Model上，Model通过View-Model的 Data Bindings 来管理View中的数据，View-Model就是从中起到一种桥梁的方式（也就是现在的 `Vue`、`React` 框架所做）


特点是：
- 实现视图和数据分离
- 通过数据驱动视图，开发者只需关心数据变化，不需要关心DOM操作


核心：
- 响应式
- 模板编译
- 渲染

