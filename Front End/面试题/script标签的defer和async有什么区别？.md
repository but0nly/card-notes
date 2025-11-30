#面试题 

就跟他们的名称一样
defer代表延迟
async代表同步

- 不加属性的script标签，HTML暂停解析，然后下载js、解析js，再继续解析HTML
- 加了defer属性的script标签，HTML解析，并行下载JS，HTML解析完成后，解析JS
- 加了async属性的script标签，HTML解析，并行下载JS，JS下载完成后暂停HTML解析，解析JS完毕后继续解析HTML