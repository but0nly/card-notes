#面试题 


### 简单描述
- 握手是链接 
- 挥手是告别

### 建立TCP链接
- 先建立链接（确保对方有接收消息的能力）
- 再传输内容（如发个GET请求）
- 网络协议是TCP 传输协议是HTTP


### 三次握手

1. Client 发送 Sever 接受； Sever： Client要建立链接
2. Sever 发送 Client 接受；Client：Sever知道了
3. Client 发送 Sever 接收；Sever：Client要准备发送了


### 四次挥手

1. Client 发送 Sever接受； Sever：Client 要断开链接
2. Sever 发送 Client接收；Client：Sever知道了，等待Sever忙完
3. Sever 发送 Client接受；Client：Sever已经忙完，可以关闭链接
4. Client 发送 Sever接收；Sever：可以关闭链接了，然后断开链接