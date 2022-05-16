# React 系列之 useState

基本用法  
 `const [state, setState] = useState(initialState);`
当然也可以写成
`const state = useState(initialState)`
state 为数组 state[0]为状态值 state[1]为更新状态的函数
我们知道 useState 跟新状态时为异步更新，setState 又没有跟之前版本提供回调，当想要同步获取最新值时可以这样
`useEffect(() => {`
`TODO 处理你的逻辑`
`}, [state])`
但是这个方法会在初始化时执行
`setState(() => {`
`TODO 处理你的逻辑`
`return newState`
`})`
newState 为想要改变的最新值，在这个回调中处理逻辑

多次 setState 时 React 会自动合并成一次 setState，但是有些情况下是不会的，这时就需要使用
ReactDOM.unstable_batchedUpdates 这个 api 来手动处理多次合并一次

# React 系列中 useEffect

useEffect 是可以让你在函数组件中执行副作用操作(相当于类组件中生命周期函数)
它可以看作是三个生命周期函数的组合
1、componentDidMount
`useEffect(() => {}, [])`
组件生命周期内执行一次
2、componentDidUpdate
`useEffect(() => {}, [state])`
此写法也会在初始化时执行，state 变化时再次执行
3、componentWillUnMount
`useEffect(() => {`
` return () => {`
` //TODO 组件销毁前执行`
` }`
`}, [])`

# useEffect 有哪些注意点

1、假如说 useEffect 监听了多个 state,同事更新多个 state 情况会导致 useEffect 中函数执行多次，这样就需要特别处理多个 state 合并一个或者在里面进行判断(业务场景复杂多样，具体还是要在设计之初就考虑进去)  
 2、禁止在条件语句中使用
`if (name !== 'xx') {`
` useEffect(() => {}, [])`
`}`

# useMemo

在方法函数，由于不能使用 shouldComponentUpdate 处理性能问题，react hooks 新增了 useMemo
用来缓存数据，当渲染的数据需要根据 state、props 经过特定计算而来的时候可以使用 useMemo 函数缓存这个数据、避免重复调用计算函数浪费性能
`const x = useMemo(() => {`
`//TODO`
`}, [xx])`
如果 useMemo(fn, arr)第二个参数发生变化，则去执行 fn 否则只会执行一次，[]也是执行一次

# useCallback

用来监听变量缓存或生成一个函数，fn 通常当作 props 进行传递用于子组件进行监听！
`const fn = useCallback(() => {`
`//TODO`
`}, [xx])`
``

# useContent

全局上下文配合 usereducer 可以做到全局的状态管理 替代 mobx、redux
`function createContainer(useHook){`
` const Context = react.createContext(null)`
` const Provider = props => {`
` const value = useHook(props.initialValue)`
` retrun (`
` <Context.Provider value={value}>`
` {props.children}`
` </Context.Provider>`
` )`
` }`
` const useContainer = () => {`
` const value = React.useContext(Context)`
` return value`
` }`
` return {`
` Provider,`
` useContainer`
` }`

`const fn = createContainer(() => {`
` const reducer = (state, action) => {`
` switch(action.type) {`
` case 'xx':`
` return {...state, xx: action.xx}`
` break;`
` }`
` })`
` const initState = {`
` xx: xx`
` }`
` const [state, dispatch] = useReducer(reducer, initState)`
` return {`
` state, dispatch`
` }`
最外围组件使用
`<Logic.Provider>xxxx</Logic.Provider>`
组件内使用 先引入
`const { state, dispatch } = Logic.useContainer()`

# diff 算法

传统 diff 算法，需要遍历整棵树的节点然后进行比较，是一个深度递归的过程，运算复杂度常常是 O(n^3)
react 中 diff 采用了优化策略使运算复杂度降到 O(n)
1、忽略 Web UI 中 DOM 节点跨层级移动；
2、拥有相同类型的两个组件产生的 DOM 结构也是相似的，不同类型的两个组件产生的 DOM 结构则不近相同
3、对于同一层级的一组子节点，通过分配唯一唯一 id 进行区分（key 值）
三个优化
1、tree diff
基于策略一，React 的做法是把 dom tree 分层级，对于两个 dom tree 只比较同一层次的节点，忽略 Dom 中节点跨层级移动操作，只对同一个父节点下的所有的子节点进行比较。如果对比发现该父节点不存在则直接删除该节点下所有子节点，不会做进一步比较，这样只需要对 dom tree 进行一次遍历就完成了两个 tree 的比较
2、component diff
React 应用是基于组件构建的，对于组件的比较优化侧重于以下几点：
1). 同一类型组件遵从 tree diff 比较 v-dom 树
2). 不通类型组件，先将该组件归类为 dirty component，替换下整个组件下的所有子节点
3). 同一类型组件 Virtual Dom 没有变化，React 允许开发者使用 shouldComponentUpdate（）来判断该组件是否进行 diff，运用得当可以节省 diff 计算时间，提升性能
3、element diff
对于同一层级的 element 节点，diff 提供了以下 3 种节点操作：  
1). INSERT_MARKUP 插入节点：对全新节点执行节点插入操作
2). MOVE_EXISING 移动节点：组件新集合中有组件旧集合中的类型，且 element 可更新，即组件调用了 receiveComponent，这时可以复用之前的 dom，执行 dom 移动操作
3). REMOVE_NODE 移除节点：此时有两种情况：组件新集合中有组件旧集合中的类型，但对应的 element 不可更新、旧组件不在新集合里面，这两种情况需要执行节点删除操作

# 设计模式

# react 生命周期

# react 中高阶组件运用了什么设计模式

使用了装饰器模式，装饰模式的特点是不需要改变 被装饰对象 本身，而只是在外面套一个外壳接口。

## 函数组件优化

使用 React.memo()对组件进行优化，跟 PureComponet 效果一样，浅比较 props。需要深层比较需要在这个函数传入第二个比较函数它有两个参数，preProps，nextProps
