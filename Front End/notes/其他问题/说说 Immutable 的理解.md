#面试题 

语义化就是不可变的意思，对 ***Immutable*** 对象做的任何*增删改*都会返回一个新的 ***Immutable*** 对象


### 应用场景
React PureComponent 和 Redux：避免不必要的渲染。
因为React 和 Redux 进行状态比较时，深度对比是非常耗时跟耗性能的。如果使用Immutable只需要对比应用即可(如果一个值没有发生变化，那么他的引用也不会变)。