# 每日一题

## bind、call、apply三者有什么异同
  1、三者都是改变传入函数的this指向
  2、call、apply都是立即执行函数改变本次函数调用的this指向
  3、call方法传参是参数列表形式、apply方法传参是数组形式
  4、bind方法是返回一个永久改变this的新函数，传参方式是参数列表形式
## 看如下代码写出a是什么及打印结果
  `if (a == 1 && a == 2 && a == 3){`
  `  console.log(a)`
  `}`
  答案valueOf版本
  `const a = {`
  `  value: 1,`
  `}`
  `a.__proto__.valueOf = function () {`
  `  return a.value++`
  `}`
  `a = {value: 4}`
  答案tostring版本
  `const a = [3, 2, 1]`
  `a.__proto_.toString = function () {`
  `  return a.pop()`
  `}`
  ` a = []`
  使用了js中自动转换调用valueOf/toString

## React生命周期及其作用
  constructor:
    1、用于初始化内部状态，很少使用
    2、唯一一个可以直接修改state的地方

## 开发中常用api
Array篇
`[].map(it => return it) //返回一个新数组`
`[].indexOf(it) //返回的是当前元素的下标 没有则返回-1`
`[].includes(it) //判断当前元素是否在数组内`
`[].concat([]) //拼接两个数组 返回拼接后新数组`
`[].splice(index, length, item) //获取从index开始有length数的数组 item有值则会添加到原数组中`
`[].sort((a, b) => a-b) //从小到大 b-a从大到小`
`[].reduce((pre, next) => pre+next) //数组求和`
`[].find(it => it) //从数组中查找某一个符合条件的元素 找不到为undefined`
`[].filter(it => it) //从数组中筛选符合条件的元素 找不到为[]`
`[].forEach(it => console.log(it)) //遍历这个数组`
`[].push(it) //向数组尾部添加一个元素`
`[].pop() //尾部弹出一个元素 返回弹出的元素 原数组改变`
`[].shift() //数组头部弹出一个元素 返回弹出的元素 原数组改变`
`[].unshift //数组头部添加一个元素 原数组改变`
`[1,[2,[3]]].flat(2) => [1,2,3] //打平一个多维数组 参数是层级 返回新数组原数组不变`
Object篇
`Object.prototype.toString(arg) //可用于判断元素是什么类型`
`Object.keys(arg) //返回这个对象所有属性的数组`
`Object.values(arg) //返回这个对象所有属性值的数组`
`Object.defineProperties(obj, props) //方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象 Vue3之前最重要的一个api`
``
## typeof 
typeof 是用于检测左侧对象是否是右侧对象的子集

## 关于使用React.lazy的问题
  使用React.lazy进行加载组件不做处理会报错A React component suspended while rendering, but no fallback UI was specified.
  错误原因是用lazy 之后, 存在加载中的空档, react 不知道在这个空当中该显示什么, 所以需要我们指定
  解决办法
    使用 Suspense 组件包裹路由组件、进行提示加载的空档做什么
    `<Suspense`
    ` fallback={`
    `   <Spin spinning>`
    `      <div style={{ width: '100%', height: '100vh' }} />`
    `   </Spin>`
    ` }`
    `>`
    `  <Router>`
    `    <Switch>`
    `      <Route path="/create" component={Create}/>`
    `    </Switch>`
    `  </Router>`
    `</Suspense>`




