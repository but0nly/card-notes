#面试题 

```js
const events = new EventBus();

events.on('key1', fn1);
events.on('key1', fn2);
events.once('key1', fn3);

events.emit('key1') // fn1 fn2 fn3

events.emit('key1') // fn1 fn2 // 这里的fn3在上一次触发已经被清除

events.off('key1')

```

### 功能
- `on`（注册事件）
- `once` (注册事件，触发一次就清除)
- `emit`（触发事件， 包含参数）
- `off`（清除事件， 用第二个参数可清除事件单个函数）

### 代码实现

```js

class EventBus{
  events = {
    // 'key': { fn: Function, isOnce: Boolean}
    //...
  }

  on(key, fn, isOnce = false){
    if(this.events[key] == null){
      // 初始化事件
      this.events[key] = []
    }

    this.events[key].push({fn, isOnce})
  }

  once(key, fn){
    this.on(key, fn, true)
  }

  emit(key, ...args){
    const fnList = this.events[key]
    if(fnList == null) return;

    this.events[key] = fnList.filter(event=>{
      const { fn, isOnce} = event
      fn(...args);

      if(isOnce) return false // 执行一次后删除
      return true
    })
  }


  off(key, fn){
    if(this.events[key] == null) return;

    if(fn){
      const fnList = this.events[key]
      if(fnList){
        this.events[key] = fnList.filter(event=> event.fn !== fn); // 清除单个函数
      }
    }else{
      this.events[key] = [] // 清除
    }
  }
}

const events = new EventBus();

function fn1(params) {
  console.log('fn1');
}

function fn2(params) {
  console.log('fn2');
}

function fn3(params) {
  console.log('fn3');
}

events.on('key1', fn1);

events.on('key1', fn2);

events.once('key1', fn3);

events.emit('key1') // fn1 fn2 fn3

events.emit('key1') // fn1 fn2 // 这里的fn3在上一次触发已经被清除

events.off('key1', fn2); // 清除fn2

events.emit('key1') // fn1
  
events.off('key1') // 全部清空

```