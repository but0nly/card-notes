#面试题 
**React** 事件模拟出来 *DOM* 事件所有能力

- **React** 事件中的 `event` 继承的是 *Synthetic Events*
- 并非原生事件 *MouseEvent*
- 但是在 **React** 事件中 event 的 nativeEvent 指向就是原生事件
	- 注意React 时间中的event.nativeEvent.currentTarget事件是绑定在document的（在react 17版本就不再绑定到document）





### 区别
- event 是 Synthetic Events（合成事件），模拟 DOM事件所有能力
- event 的 nativeEvent 是原生事件
- 所有的事件，都被挂载在document上
- 和DOM事件不一样， 和Vue事件也不一样（Vue事件是绑定在当前元素）