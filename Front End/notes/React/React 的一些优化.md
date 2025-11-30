#面试题 

- 使用CSS模拟v-show
- 循环列表添加key，减少渲染次数
- 使用Fragment作为组件最外层，减少层级
- 不在JSX中定义函数
- 不在JSX中使用bind(this)
- 不可变数据
- 使用shouldConponentUpdate判断组件是否要更新
	- 或者使用React.PureComponent
	- 函数组件使用React.Memo
- Hooks缓存数据和函数
	- useMemo
	- useCallback
- 路由懒加载（bundl-loader）