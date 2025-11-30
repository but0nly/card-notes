#面试题 


- watch 是监听单个值，watchEffect可以监听多个值
- watch 申明比较明确，watchEffect 需要观察函数里面的值
- watch 页面创建时不会触发（需要加第三个参数，{immediate: true}）
- watch 可以拿到新的值，watchEffect 拿不到




### 应用
需要用到新值时，用watch
