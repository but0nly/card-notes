#面试题 

## 跨域请求
---
- 浏览器机制
	- 同源策略，不允许你去请求第三方域名的一些东西（一般就是获取服务端的数据）
- 同源策略
	- 一般限制Ajax网络请求，不能跨域请求server
- 不会现在`<link><img><script><iframe>`加载第三方资源


## 解决跨域
---
- JSONP （服务端）
- CORS 配置允许跨域（服务端）
	- `Response.setHeader("Access-control-Allow-Origin", "http://loaclhost:8080")` 设置值为要跨域的域名，可以设为`*`



## 多余的`options`请求
---
- `options`请求，是跨域之前的预检查（检查`Access-control-Allow-`相关的配置）
- 浏览器自行发起的，无须我们干预
- 不影响实际功能