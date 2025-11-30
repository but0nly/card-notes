#面试题 


当我们执行任意 React上下文函数（anyMethod）的时候会触发事务机制，
把我们要执行的函数包裹一层，

步骤如下
- 执行preform（anyMethod）
- 执行initialize
- 执行anyMethod
- 再执行close