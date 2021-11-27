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
## 检测类型的方法
typeof 使用来判断检测对象的属性 但是typeof null 返回的是object、并非是bug只是js设计如此、区分数组跟对象时不能正确判断
instanceof 用来检测左侧引用的__proto__是否在右侧对象的Ptototype上，通过原型链查找故这个方法不能判断基本数据类型
Object.prototype.toString.call(param) 返回具体是什么类型，适用所有类型
通过构造函数指向判断 
  `let a = 123`  
  `a.constructor === Number // true`


## hash路由跟history路由的区别
1、直观来看hash就是url中带#号history不带
2、hash监听url中hash值的变化(#号后面的内容),不向服务器发送请求就可以改变页面展示
   history则是监听url整体变化，回去请求服务端需要两端共同支持
3、hash是支持低版本浏览器的，#号后面值的变化都会触发window.onhashchange,不论浏览器的
  前进还是后退都会触发
  history则是基于Html5新增API产生的

  

## px、rem、em有什么区别
px代表像素，相对长度单位，像素px是相对于显示器屏幕分辨率而言的，1px就是屏幕上的一个小方格点
rem相对单位，相较于页面根元素大小而定，在做适配时常用，只需要改变跟元素大小就能调整所有字体大小
em相对单位，相对于最近父元素大小而言，如未设置则取浏览器默认大小

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
## 常见状态码
  400 请求无效
  403 禁止访问 无权限
  404 资源找不到、路径错误或者没有要请求的资源
  405 资源被禁止
  408 资源超时
  200 请求ok
  502 请求方法不匹配
  500 服务器出错

## webpack优化手段
  1、优化loader查找范围 例如Babel只转换src下的文件
  2、cache-loader缓存loader处理结果
  3、多线程处理打包  
  4、删除无用css    purgecss-webpack-plugin 配合 mini-css-extract-plugin使用
  5、以CDN方式加载资源   add-asset-html-cdn-webpack-plugin插件
  6、对图片进行压缩优化  image-webpack-loader
  7、通过speed-measure-webpack-plugin插件查看哪个模块打包费时
  8、
## React和ReactDOM的区别
  React是React库的入口，可以使用 jsx语法、组件、ref、hooks等属性或api
  ReactDOM只负责和浏览器或DOM操作相关  

## redux与mobx的区别
  redux将数据保存在单一store中mobx分散存放的

## Promise中api
  all 顺序执行 有一个失败都为失败
  allSettled 顺序执行 可以获取每一个的状态
  race 获取第一个的状态
##   
    


