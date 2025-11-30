#面试题 

### 定义
是一个延迟执行操作。当事件被频繁触发的时候，延迟执行事件处理函数，并且如果在延迟时间内触发会重新计算延迟时间。只有当事件没有在指定时间内再次触发，事件函数才会执行。

#### 入参
 1. 事件函数 `fn` 
 2. 延迟时间 `deley` 单位ms
#### 出参
 1. 返回新的函数

### 代码实现
思路：利用**闭包**和`setTimeout`，触发时清空`seTimeout`的ID(如果存在的话)

```js

function debounce(fn, delay) {
  let timer;
  return function(...args){
    // 如果存在计时器,代表此处是在指定时间内再次出发.所以需要从新清理定时,重新执行setTimeout
    if(timer){
      clearTimeout(timer)
    }

    timer = setTimeout(()=>{
      // 需要改掉this指向，否则就指向了window或者globalThis。
      fn.apply(this, args);
      timer = null;
    }, delay);
  }
}

const obj = {
  x: 100,
  fn: debounce(function(name){
    console.log(this, name);
  }, 1000)
};

obj.fn();
```
