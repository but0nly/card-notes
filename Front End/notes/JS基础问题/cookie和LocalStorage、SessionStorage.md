#面试题 

## Cookie
---
- 起初是用来跟服务端通信的
- 被客户端接来做 ”存储“ （html5出来之前）
- 通过`document.cookie`去存储


### 缺点

- 存储量太小，最大4kb
- http请求每次都会带上，增加请求数据量
- 只能用`document.cookie`去存储， 只有追加和覆盖，太过简陋




## LocalStorage
---
- html5专门为了设计存储而生， 最大5M
- API简单易用 getItem、setItem
- 不会被http请求发送出去
- 永久存储，除非代码或者手动删除



## SessionStorage
---
- 同上
- 只存储在当前回话，浏览器关闭则清空






## 三者的区别
---

- 容量
- API易用性
- 是否被http请求发送