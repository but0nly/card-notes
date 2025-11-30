#面试题 

### 旧的Methods

> http/1.0 阶段
- get
- post

### 新的Methods

> http/1.1 阶段
- `get`
- `post`
- `patch/put`
- `delete`




### **RESTful API**
> 正是http/1.1 的新特性

- 是一种新的API设计方法
- 传统API设计： 把每个url当作一个功能
- **RESTful API**：把每个url当作一个资源
	- 尽量不用url参数
	- 用method表示操作类型

传统api的url
- /api/list?pageIndex=2

**RESTful API**
- /api/list/2


