与Effect一样，但是它是在DOM更新之前更新。

用于`css-in-js`，为了解决注入样式的性能问题而出现

### useEffect\useLayoutEffect\useInsertionEffect三者的执行顺序
useInsertionEffect(DOM更新之前) > useLayoutEffect（DOM更新之后、浏览器绘制之前） > useEffect（浏览器绘制之后）