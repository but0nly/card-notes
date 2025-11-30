#面试题 



```jsx
render(){
	return <div onClick={this.handlerClick.bind(this, y, x)}></div>
}

handlerClick(y, x, event){
	console.log(event); // Synthetic Event
}
```