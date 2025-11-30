#面试题 

```jsx
handlerClick(){
	console.log('点击了')；
	this.setState({
		
	})
}
<div onClick={this.handlerClick}></div> // 此时的handlerClick中的this执行undefined
<div onClick={this.handlerClick.bind(this)}></div>

```
因为赋值问题，导致this丢失

### 原因
[[Class 类中的静态方法和原型方法绑定this]]





### 除了使用bind还可以用箭头函数

始终指向class的this

```jsx
handlerClick = () => {
	console.log('点击了')；
	this.setState({
		
	})
}
<div onClick={this.handlerClick}></div> // 此时的handlerClick中的this执行undefined
<div onClick={this.handlerClick.bind(this)}></div>

```