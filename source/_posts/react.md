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

  多次setState时React会自动合并成一次setState，但是有些情况下是不会的，这时就需要使用
  ReactDOM.unstable_batchedUpdates 这个api来手动处理多次合并一次


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
# useMemo
  在方法函数，由于不能使用shouldComponentUpdate处理性能问题，react hooks新增了useMemo
  用来缓存数据，当渲染的数据需要根据state、props经过特定计算而来的时候可以使用useMemo函数缓存这个数据、避免重复调用计算函数浪费性能
  `const x = useMemo(() => {`
  `//TODO`
  `}, [xx])`
  如果useMemo(fn, arr)第二个参数发生变化，则去执行fn 否则只会执行一次，[]也是执行一次

# useCallback
  用来监听变量缓存或生成一个函数，fn通常当作props进行传递用于子组件进行监听！
  `const fn = useCallback(() => {`
  `//TODO`
  `}, [xx])`
  ``
# useContent
  全局上下文配合usereducer可以做到全局的状态管理 替代mobx、redux
  `function createContainer(useHook){`
  `  const Context = react.createContext(null)`
  `  const Provider = props => {`
  `    const value = useHook(props.initialValue)`
  `    retrun (`
  `      <Context.Provider value={value}>`
  `        {props.children}`
  `      </Context.Provider>`
  `    )`
  `  }`
  `  const useContainer = () => {`
  `    const value = React.useContext(Context)`
  `    return value`
  `  }`
  `  return {`
  `    Provider,`
  `    useContainer`
  `  }`

  `const fn = createContainer(() => {`
  `  const reducer = (state, action) => {`
  `    switch(action.type) {`
  `      case 'xx':`
  `        return {...state, xx: action.xx}`
  `        break;`
  `    }`
  `  }) `
  `  const initState = {`
  `    xx: xx`
  `  }`
  `  const [state, dispatch] = useReducer(reducer, initState)`
  `  return {`
  `    state, dispatch`
  `  }`
  最外围组件使用
  `<Logic.Provider>xxxx</Logic.Provider>`
  组件内使用 先引入
  `const { state, dispatch } = Logic.useContainer()`
# diff算法

# 设计模式


# react 生命周期



