#面试题 


- JS无法直接调用native API
- 需要一些特定的"格式"来调用
- 这些特定的“格式”就叫作 Js Bridge， 例如微信的js-sdk

![[Pasted image 20230920155153.png]]


## JS Bridge的常用方法
---

- 注册全局API
- URL Scheme （推荐）
	- 例如 weixin://scan（扫一扫）
	- App会先检查写的协议是否符合制定的协议，是的话，app就给你调用那些功能，
