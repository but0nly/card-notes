#面试题 

### 定义
是一个限制函数触发频率的技术。当事件被频繁触发时，在时间间隔内只会被执行一次。即在一个时间段内只会执行一次事件函数。

#### 入参
 1. 事件函数 `fn` 
 2. 时间间隔 `time` 单位ms
#### 出参
 1. 返回新的函数

### 代码示例
**思路**：利用**闭包**和`setTimeout`，如果`timer`存在就不执行。

```js
function throttle(fn, time) {
  let timer
  return function (...args) {
    if(!timer){
      timer = setTimeout(()=>{
        fn.apply(this, args);
        clearTimeout(timer)
        timer = null
      }, time)
    }
  }
}

let count = 0
const click = throttle(()=>{
  count++
  console.log(`触发了${count}次`);
}, 1000);


// 模拟点击
function simulation() {
  click();

  setTimeout(()=>{
    click()
  }, 500);
}

simulation(); // 触发了1次

```