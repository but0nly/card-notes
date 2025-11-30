#面试题 


语法

```js
const [name, setName] = useState('名字')

useMemo(()=>{
	return { name, age: 20}
}, [name]) // 依赖响应对象，当依赖数据更新，useMemo中的缓存的数据也会被更新
```

- react 会默认更新所有子组件
- class组件 使用的SCU和PureComponent
- Hooks组件使用 useMemo
