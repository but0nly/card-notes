#面试题 




### request header
- accept  浏览器接受的资源
- accept-encoding 浏览器接受的压缩算法，如gzip
- Accept-Language 浏览器接受的语言
- Connection：keep-alive； 支持长连接， 一次TCP连接多次请求
- Cookie
- Host 请求的域名
- User-Agent 浏览器的信息
- Content-type 发送的数据格式, 如application/json（get请求没有）





### response header
- Content-type 返回的数据格式, 如application/json（get请求没有）
- Content-length 返回的数据大小，多少字节
-  accept-encoding 返回数据的压缩算法，如gzip




### 自定义header的应用

- 用于加密通信



### 缓存相关的header

- Cache-Contorl    Expires
- Last-modified     If-modified-Since
- Etag                     If-None-Match