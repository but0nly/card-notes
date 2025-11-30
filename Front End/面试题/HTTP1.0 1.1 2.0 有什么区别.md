#面试题 

## HTTP1.0
---
- 最基础的HTTP协议
- 支持基本的`GET`、`POST`请求


## HTTP1.1
---
- 支持新的方法`PUT`、`DELETE`，可以用于Result API
- 支持长连接 `Connection：keep-alive`，一次TCP请求，支持多次请求
- 缓存策略 `cache-control` 、`E-tag`等
- 断点续传，状态码206
	- 上传视频或者图片的时候，分段上传
	- 上传一段后，服务端放回206
	- 直到全部上传后，返回状态200

## HTTP2.0
---
- 多路复用，一次TCP请求，支持多个并行请求
- 压缩Header，减少体积
- 服务端推送