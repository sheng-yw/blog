# React系列之useState
  基本用法  
  `const [state, setState] = useState(initialState);`
  当然也可以写成
  `const state = useState(initialState)`
  state为数组 state[0]为状态值 state[1]为更新状态的函数
  我们知道useState跟新状态时为异步更新，setState又没有跟之前版本提供回调，当想要同步获取最新值时可以这样
  `useEffect(() => {`
    `TODO 处理你的逻辑`
  `}, [state])`
  但是这个方法会在初始化时执行
  `setState(() => {`
    `TODO 处理你的逻辑`
    `return newState`
  `})`
  newState为想要改变的最新值，在这个回调中处理逻辑
## 关于优化
  setState为异步更新调用一次渲染一次，所以在一个方法内调用多个不同的setState时会导致许多不必要的性能消耗！解决办法我总结了一下两点
  1、把多个state合并成一个state
  2、使用React中自带api解决
    `ReactDOM.unstable_batchedUpdates(() => {`
      `setState1(xxx)`
      `setState2(xxx)`
    `})`

# React系列中useEffect
  useEffect是可以让你在函数组件中执行副作用操作(相当于类组件中生命周期函数)
  它可以看作是三个生命周期函数的组合
  1、componentDidMount
    `useEffect(() => {}, [])`
    组件生命周期内执行一次
  2、componentDidUpdate
    `useEffect(() => {}, [state])`
    此写法也会在初始化时执行，state变化时再次执行
  3、componentWillUnMount
    `useEffect(() => {`
    `  return () => {`
    `    //TODO 组件销毁前执行`
    `  }`
    `}, [])`
# useEffect有哪些注意点
  1、假如说useEffect监听了多个state,同事更新多个state情况会导致useEffect中函数执行多次，这样就需要特别处理多个state合并一个或者在里面进行判断(业务场景复杂多样，具体还是要在设计之初就考虑进去)    
  2、禁止在条件语句中使用
    `if (name !== 'xx') {`
    `  useEffect(() => {}, [])`
    `}`