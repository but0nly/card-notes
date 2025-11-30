#面试题 

## ErrorBoundary（错误拦截）
---

主要是使用getDerivedStateFromError方法监听渲染错误，并设置state，然后配合componentDidCatch上报错误


- 不能监听到DOM渲染报错
- 事件报错用trycatch或者window.onerror
- 异步报错用window.onerror


