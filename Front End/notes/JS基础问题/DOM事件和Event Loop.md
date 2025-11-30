#面试题 


- JS是单线程
- 异步（setTimeout、 ajax等）使用回调，基于Event Loop
- DOM事件也是基于EventLoop
	- 如click事件，等待用户点击的时候放到callback queue中；