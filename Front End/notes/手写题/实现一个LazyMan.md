#面试题 

看题
```js

const man = new LazyMan('杰克')；
man.eat('苹果').eat('梨子').eat('西瓜').sleep(5).eat('桃子')

// 苹果
// 梨子
// 西瓜
// 等待5s
// 桃子

```



思路
- 创建一个tasks，每次调用方法把task push 到 tasks
- 执行next，把任务shift出来执行
- 遇到sleep, 调用setTimeout


实现
```js


class LazyMan(){
	tasks = []; // 任务队列
	name;

	constructor(name){
		this.name = name;

		//异步调用this.next()
		setTimeout(()=>{
			this.next()
		})
	}

	next(){
		// 取出下一个任务执行
		const task = this.tasks.shift()；
		if(task) task()
	}

	eat(fruit){
		// 创建任务
		const task = function(){
			console.log(`${this.name} 吃 ${fruit}`);
			// 执行下一个任务
			this.next()
		}
		// 把task推进队列中
		this.tasks.push(task);

		// 返回实例本身,用于链式调用
		return this
		
	}


	sleep(second){
		// 创建任务
		const task = function(){
			setTimeout(()=>{
				//使用setTimeout延迟执行
				console.log(`等待了${5}秒`)
				this.next()
			}, second * 1000)
		}
		// 把task推进队列中
		this.tasks.push(task);

		// 返回实例本身
		return this
	}
}

```