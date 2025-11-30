#面试题 

react 中从编译到渲染， jsx -> Element -> FiberNode -> DOM

首先Hooks要和一个函数组件绑定，就要和这个转换的某个节点关联，由于Hooks只有在render的时候才会调用，所以只能关联到FiberNode中。

FiberNode中有一个属性 memoizedState，这个属性在Class组件中对应的是最终渲染的state。

Class组件的state是一个对象，而函数组件的state是一个链表如：
```js
memoizedState = {a: 1, b: 2} => 函数组件 memoizedState = {state: 1, next: {state: 2, next: ..}}
```


每个链表的节点都是一个 `useState`， 从而将所有 Hooks 串联起来，不仅仅 State Hook，其它 Hook 也是通过 `memoizedState` 串联起来的。

第一次渲染的时候，通过 `Fider` 的 `memoizedState` 将所有的 Hooks 收集。

当执行 setState 组件更新时，会重新执行函数组件，这时会将收集起来的Hooks按照执行顺序取出，对于 State Hook 会进行计算最新值取出，Effect Hook 会在渲染完成后执行Effect return 的函数，再执行 Effect 副作用函数