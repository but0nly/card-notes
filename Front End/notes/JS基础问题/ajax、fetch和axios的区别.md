#面试题 
三个都用于网络请求，但是维度不同

- ajax 
	- 是一个技术统称
- fetch
	- 是一个浏览器的原生API
	- 跟XHR一个级别
	- 支持Promise
	- 不支持abort
	缺点：HTTP返回错误的状态码，它不会将Promise的状态标记为reject
- axios
	- 是一个第三方库
	- 使用XMLHTTPRequest实现
