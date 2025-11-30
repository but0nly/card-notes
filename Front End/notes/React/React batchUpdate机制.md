#面试题 

它是setState中的一个机制，影响setState是否批处理和异步、同步

- 当我们setState(newState)的时候
- newState会进去到pending队列中
- 判断是否命中batchUpdate
	- 是：保存组件于dirtyComponents中
	- 否：遍历所有的dirtyComponents 调用updateComponent 更新pending state or props




### isBatchingUpdate
`isBatchingUpdate` 用来确定是否处于 *BatchUpdate* 中

处于 *BatchUpdate* 中：
```js
  componentDidMount() {
    // 开始 处于BatchUpdate中
    // isBatchingUpdates = true;

    this.setState({ // 这时isBatchingUpdate 是true, 异步执行
      value: 'value'
    })

    // isBatchingUpdates = false
  }
```


不处于BatchUpdates中：
因为setTimeout异步执行，所以执行setState时isBatchingUpdates = false；
```js
  componentDidMount() {
    // 开始 处于BatchUpdate中
    // isBatchingUpdates = true;

    setTimeout(()=>{// 因为setTimeout异步执行，此时isBatchingUpdates = false
	    this.setState({ // 同步执行，不会合并
	      value: 'value'
	    })
    }, 500)

    // isBatchingUpdates = false
  }
```



### 哪些能命中BatchUpdates机制

- 生命周期
- React 中注册的事件（onClick， onChange）
- React 可以管理的“入口”


### 哪些不能命中BatchUpdates机制

- setTimeout、setInterval等
- 自定义DOM事件
- React 不能管理的 “入口”
