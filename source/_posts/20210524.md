# React系列中useEffect

# 什么是useEffect
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