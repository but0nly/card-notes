#面试题 


- Block Format Context 块级格式化上下文
- 内部的元素无论怎么改动，都不会影响其他元素的位置


## 触发BFC条件
---
- 根节点 `<html>`
- float：left/right
- overflow: auto/hidden/scroll；
- display：inline-block；
- position：absolute/fixed
- diaplay：flex/grid