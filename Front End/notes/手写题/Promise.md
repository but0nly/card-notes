#面试题 

`Promise`是一个对象，它代表了一个异步操作的最终完成或者失败；

- 为了解决异步回调 callback hell（回调地狱）
- 把嵌套模式变成管道模式


## 三种状态
---
- pending   (进行中)
- resolved（完成）
- rejected （失败）

- pending -> resoleved 或者 pending -> rejected
- 变化不可逆



### 状态的表现

- pending状态 不会触发then和catch
- resolved状态 会触发后续的then函数
- rejected状态 会触发后续的catch函数


### then和catch改变状态

- then正常返回resolved状态，内部报错返回rejected状态
- catch正常返回rejected状态，内部报错返回resolved状态



### 初始化 promise 时，传入的函数会立马被执行

```js
new Promise(function(resolve){ // 立马被执行
	console.log('1')
	resolve(2) // 执行resolve()
}).then((res)=>{ // 异步回调， 微任务
	console.log(res) // 2
})



```


### 实现一个简易promise
```js




class CustomPromise{
  state = 'pending';   // pending fulfilled rejected
  value = undefined; // 成功后的值
  reason = undefined; // 失败后的值
  resolveCallbacks= []; // 在pending状态下,存储成功的回调
  rejectCallbacks =[]; // 在pending状态下,存储失败的回调
  
  constructor(fn){

    const resolveHandler = (res) => {
      if(this.state === 'pending'){
        this.state = 'fulfilled';
        this.value = res;
        this.resolveCallbacks.forEach(fn=>fn(this.value))
      }
    }

    const rejectHandler = (res) => {
      if(this.state === 'pending'){
        this.state = 'rejected';
        this.reason = res;
        this.rejectCallbacks.forEach(fn=>fn(this.reason))
      }
    }

    try {
      fn(resolveHandler, rejectHandler)
    } catch (error) {
      rejectHandler(error)
    }

  }

  then(fn1, fn2){
    fn1 = typeof fn1 === 'function' ? fn1 : (v)=>v;
    fn2 = typeof fn2 === 'function' ? fn2 : (e)=>e;

    // pendind的时候存储起来
    if(this.state === 'pending'){
      return new CustomPromise((resolve, reject)=>{
        this.resolveCallbacks.push(()=>{
          try {
            const newValue = fn1(this.value);
            resolve(newValue)
          } catch (error) {
            reject(error)
          }
        })


        this.rejectCallbacks.push(()=>{
          try {
            const newReason = fn2(this.reason);
            reject(newReason)
          } catch (error) {
            reject(error)
          }
        })
      })

    }

    // fulfilled直接执行
    if(this.state === 'fulfilled'){
      return new CustomPromise((resolve, reject)=>{
        try {
          const newVal= fn1(this.value);
          resolve(newVal)
        } catch (error) {
          reject(error)
        }
      })
    }

    // rejected 直接执行
    if(this.state === 'rejected'){
      return new CustomPromise((resolve, reject)=>{
        try {
          const newReason= fn2(this.reason);
          reject(newReason)
        } catch (error) {
          reject(error)
        }
      })
    }


  }

  catch(fn){ // then的一个语法糖
    this.then(null, fn)
  }

  
}


CustomPromise.resolve = function (value) {
  return new CustomPromise((resolve)=>resolve(value))
}

CustomPromise.reject = function (value) {
  return new CustomPromise((resolve,reject)=>reject(value))
}


CustomPromise.all = function(promiseList = []) {
  return new CustomPromise((resolve, reject)=>{
    let result = [];
    let count = 0;

    promiseList.forEach(p=>{
      try {
        p.then((value)=>{
          result.push(value);
          count+=1;
  
          if(count === promiseList.length){
            resolve(result)
          }
        }).catch((error)=>{
          reject(error)
        })
      } catch (error) {
        reject(error)
      }
    })
  })
}




const p = new CustomPromise((resolve, reject)=>{
  setTimeout(()=>{
    resolve(100)
  }, 2000)
})

const p1 = CustomPromise.resolve(1000)
const p2 = CustomPromise.reject('错误信息')

// p.then(res=>{
//   console.log(res, '11');

//   return 100 + 1
// }).then((res)=>{
//   console.log(res);
// })
// console.log();


CustomPromise.all([
  p, p1, p2
]).then(ress=>{
  console.log(ress);
}).catch((err)=>{
  console.log(err);
})


```