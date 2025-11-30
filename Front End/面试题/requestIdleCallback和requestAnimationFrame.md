#面试题 


## 由 React fiber 引起关注
---

- 组件树转换成链表， 可分段渲染（分片渲染）
- 渲染时可以暂停，去执行其他高优任务，空闲时再渲染
- 如何判断空闲时间？  ———requestIdleCallback

## 区别
---

- requestAnimationFrame 每次渲染完成之后执行，高优先级
	- 每秒60帧，人眼看起来才不卡顿
	- 一帧就是16.6ms
	- 帧渲染完成之后执行
- requestIdleCallback 空闲时间执行，低优先级
	- 网页渲染比较繁忙的时候， 一帧挨一帧渲染根本没有空闲时间，不会执行



## 宏任务
---

两者都是宏任务
因为都是渲染后执行
requestAnimationFrame 比 requestIdleCallback 优先级高