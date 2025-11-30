#面试题 


1. DNS解析（得到IP），建立TCP连接（三次握手）
2. 得到HTML源码（这个时候还是字符串）
3. 浏览器解析HTML源码
4. 解析HTML过程中，遇到静态资源请求静态资源，例如JS CSS 图片 视频这些，如果是强缓存，此时不必请求
5. 字符串转换成结构化数据
6. HTML 构建DOM 树
7. CSS 构建CSSOM 树
8. 两者结合， 形成render tree 
9. Render tree 绘制到页面
10. 计算各个DOM的尺寸、定位，最后绘制到页面
11. 遇到JS可能会执行（defer、async）