# 每日一题

## bind、call、apply 三者有什么异同

1、三者都是改变传入函数的 this 指向
2、call、apply 都是立即执行函数改变本次函数调用的 this 指向
3、call 方法传参是参数列表形式、apply 方法传参是数组形式
4、bind 方法是返回一个永久改变 this 的新函数，传参方式是参数列表形式

## 看如下代码写出 a 是什么及打印结果

`if (a == 1 && a == 2 && a == 3){`
` console.log(a)`
`}`
答案 valueOf 版本
`const a = {`
` value: 1,`
`}`
`a.__proto__.valueOf = function () {`
` return a.value++`
`}`
`a = {value: 4}`
答案 tostring 版本
`const a = [3, 2, 1]`
`a.__proto_.toString = function () {`
` return a.pop()`
`}`
` a = []`
使用了 js 中自动转换调用 valueOf/toString

## React 生命周期及其作用

挂载阶段
constructor:
1、用于初始化内部状态，很少使用
2、唯一一个可以直接修改 state 的地方
getDerivedStateFromProps
render
componentDidMount
更新阶段
getDerivedStateFromProps
shouldComponentUpdate
render
getSnapshotBeforeUpdate
componentDidUpdate
卸载阶段
componentWillUnmount

## 开发中常用 api

Array 篇
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
Object 篇
`Object.prototype.toString(arg) //可用于判断元素是什么类型`
`Object.keys(arg) //返回这个对象所有属性的数组`
`Object.values(arg) //返回这个对象所有属性值的数组`
`Object.defineProperties(obj, props) //方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象 Vue3之前最重要的一个api`
``

## 检测类型的方法

typeof 使用来判断检测对象的属性 但是 typeof null 返回的是 object、并非是 bug 只是 js 设计如此、区分数组跟对象时不能正确判断
instanceof 用来检测左侧引用的**proto**是否在右侧对象的 Ptototype 上，通过原型链查找故这个方法不能判断基本数据类型
Object.prototype.toString.call(param) 返回具体是什么类型，适用所有类型
通过构造函数指向判断
`let a = 123`  
 `a.constructor === Number // true`

## hash 路由跟 history 路由的区别

1、直观来看 hash 就是 url 中带#号 history 不带
2、hash 监听 url 中 hash 值的变化(#号后面的内容),不向服务器发送请求就可以改变页面展示
history 则是监听 url 整体变化，回去请求服务端需要两端共同支持
3、hash 是支持低版本浏览器的，#号后面值的变化都会触发 window.onhashchange,不论浏览器的
前进还是后退都会触发
history 则是基于 Html5 新增 API 产生的

## px、rem、em 有什么区别

px 代表像素，相对长度单位，像素 px 是相对于显示器屏幕分辨率而言的，1px 就是屏幕上的一个小方格点
rem 相对单位，相较于页面根元素大小而定，在做适配时常用，只需要改变跟元素大小就能调整所有字体大小
em 相对单位，相对于最近父元素大小而言，如未设置则取浏览器默认大小

## 关于使用 React.lazy 的问题

使用 React.lazy 进行加载组件不做处理会报错 A React component suspended while rendering, but no fallback UI was specified.
错误原因是用 lazy 之后, 存在加载中的空档, react 不知道在这个空当中该显示什么, 所以需要我们指定
解决办法
使用 Suspense 组件包裹路由组件、进行提示加载的空档做什么
`<Suspense`
` fallback={`
` <Spin spinning>`
` <div style={{ width: '100%', height: '100vh' }} />`
` </Spin>`
` }`
`>`
` <Router>`
` <Switch>`
` <Route path="/create" component={Create}/>`
` </Switch>`
` </Router>`
`</Suspense>`

## 常见状态码

400 请求无效
403 禁止访问 无权限
404 资源找不到、路径错误或者没有要请求的资源
405 资源被禁止
408 资源超时
200 请求 ok
502 请求方法不匹配
500 服务器出错

## webpack 优化手段

1、优化 loader 查找范围 例如 Babel 只转换 src 下的文件
2、cache-loader 缓存 loader 处理结果
3、多线程处理打包  
4、删除无用 css purgecss-webpack-plugin 配合 mini-css-extract-plugin 使用
5、以 CDN 方式加载资源 add-asset-html-cdn-webpack-plugin 插件
6、对图片进行压缩优化 image-webpack-loader
7、通过 speed-measure-webpack-plugin 插件查看哪个模块打包费时

## React 和 ReactDOM 的区别

React 是 React 库的入口，可以使用 jsx 语法、组件、ref、hooks 等属性或 api
ReactDOM 只负责和浏览器或 DOM 操作相关

## redux 与 mobx 的区别

redux 将数据保存在单一 store 中 mobx 分散存放的

## Promise 中 api

all 顺序执行 有一个失败都为失败
allSettled 顺序执行 可以获取每一个的状态
race 获取第一个的状态

## CMD、AMD、CommonJS、ES6

AMD 是 RequireJS 在推广过程中对模块定义的规范化产出，AMD 规范则是非同步加载模块，允许指定回调函数。AMD 是对于依赖的模块提前执行，依赖前置
AMD 标准中，定义了下面两个 API：
`require([module], callback)`
`define(id, [depends], callback)`
即通过 define 来定义一个模块，然后使用 require 来加载一个模块。 并且，require 还支持 CommonJS 的模块导出方式。
CMD 是 SeaJS 在推广过程中对模块定义的规范化产出。CMD 是同步模块定义、是延迟执行，推崇依赖就近，即只在需要用到某个模块的时候再 require
`define(function(require, exports, module) { `
`var $ = require('jquery');`
`var C = require('./c.js');`
`exports.sayHi = ...`
`module.exports = ...`
`})`
CommonJS 规范---module.exports
其核心思想就是通过 require 方法来同步加载所要依赖的其他模块，然后通过 exports 或者 module.exports 来导出需要暴露的接口。
ES6---export/import
在 ES6 中，我们可以使用 import 关键字引入模块，通过 exprot 关键字导出模块，功能较之于前几个方案更为强大，也是我们所推崇的，但是由于 ES6 目前无法在浏览器中执行，所以，我们只能通过 babel 将不被支持的 import 编译为当前受到广泛支持的 require。

## webpack 核心

Entry：入口，Webpack 执行构建的第一步将从 Entry 开始，可抽象成输入。告诉 webpack 要使用哪个模块作为构建项目的起点，默认为./src/index.js
output ：出口，告诉 webpack 在哪里输出它打包好的代码以及如何命名，默认为./dist
Module：模块，在 Webpack 里一切皆模块，一个模块对应着一个文件。Webpack 会从配置的 Entry 开始递归找出所有依赖的模块。
Chunk：代码块，一个 Chunk 由多个模块组合而成，用于代码合并与分割。
Loader：模块转换器，用于把模块原内容按照需求转换成新内容。
Plugin：扩展插件，在 Webpack 构建流程中的特定时机会广播出对应的事件，插件可以监听这些事件的发生，在特定时机做对应的事情。

## webpack 功能

代码转换：TypeScript 编译成 JavaScript、SCSS 编译成 CSS 等等
文件优化：压缩 JavaScript、CSS、html 代码，压缩合并图片等
代码分割：提取多个页面的公共代码、提取首屏不需要执行部分的代码让其异步加载
模块合并：在采用模块化的项目有很多模块和文件，需要构建功能把模块分类合并成一个文件
自动刷新：监听本地源代码的变化，自动构建，刷新浏览器
代码校验：在代码被提交到仓库前需要检测代码是否符合规范，以及单元测试是否通过
自动发布：更新完代码后，自动构建出线上发布代码并传输给发布系统。

## 浅谈 webpack 构建流程

执行 npm run xxx 命令启动到结束会依次执行以下阶段
初始化参数：从配置文件和 Shell 语句中读取与合并参数，得出最终的参数；
开始编译：用上一步得到的参数初始化 Compiler 对象，加载所有配置的插件，执行对象的 run 方法开始执行编译；
确定入口：根据配置中的 entry 找出所有的入口文件；
编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行翻译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理；
完成模块编译：在经过第 4 步使用 Loader 翻译完所有模块后，得到了每个模块被翻译后的最终内容以及它们之间的依赖关系；
输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会；
输出完成：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统。

## js 监听 dom 变化

1、获取要监听的 dom
const dom = document.querySelector('#id')
2、创建监听对象 MutationObserver
const hanldChange = function (dom, observer) {
console.log(dom, observer)
}
const mutationObserver = new MutationObserver(hanldChange)
3、定义监听属性、开启监听
const options = {
attributes: true
}
mutationObserver.observer(dom, options)
4、停止监听
mutationObserver.disconnect()
5、清除变动记录并返回记录值
const changes = mutationObserver.takeRecords()

## package.json 中版本～ ^含义

～表示例如 1.2.2 下载最新的 1.2.x 的最新包但不会低于 1.2.2
^表示 例如 1.2.2 下载 1.x.x 的最新包 不会低于 1.2.2

## 什么是闭包

闭包的产生条件：函数嵌套，内部函数引用外部函数变量，函数执行
延长变量的生命周期
容易内存泄漏需要手动释放内存

## new 做了哪些事情

1、创建一个新的对象
2、将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）
3、执行构造函数代码(为新对象赋值)
4、有无 return，有则返回 return 的对象，无则是把当前对象返回

## z-index 失效

改变 position 为 static

## 从输入 url 到页面展示经历哪些过程

1、DNS 解析域名（先从浏览器缓存中找-系统 hosts 中-域名服务器-根域名服务器）
2、TCP 链接（三次握手 请求资源,四次挥手断开链接）
3、处理返回页面信息
4、浏览器渲染（解析标签生成 dom 树，解析 css 生成 cssom 树，两者结合生成 render 树结合 layout 进行布局绘制展示）

## script defer 和 async 有什么区别

没有 defer 或 async，浏览器会立即加载并执行指定的脚本，“立即”指的是在渲染该 script 标签之下的文档元素之前，也就是说不等待后续载入的文档元素，读到就加载并执行阻塞浏览器渲染
defer 和 async 都属于异步执行加载
async 是资源加载完毕会立刻执行，乱序的
defer 是资源加载完毕不是立刻执行，而是在元素解析完成之后，DOMContentLoaded 事件执行之前完成执行

## 强缓存协商缓存

1、强缓存：不会向服务器发送请求，直接从缓存资源中获取，状态码 200
2、协商缓存：向服务器发送请求，服务器会根据 http 请求头中字段来判断是否命中缓存，如果命中，从缓存中读取数据，返回 304 状态码
共同点：都是从客户端读取资源
强缓存需要 Cache-Control 字段，其中 max-age 属性是控制缓存最大时长(单位是秒),过期会重新发送请求。public 表示可以被任意对象缓存(客户端，代理服务器),private 表示只能在客户端缓存，no-cache 是加载资源前，强制发送请求到服务器进行协商缓存；no-store 表示不被任何缓存。
协商缓存需要用到 Etag 字段与 if-noneif-none-matc，Etag 是 HTTP 响应头中字段，Etag 值是根据资源内容编码生成的一段字符串(资源标识)，内容不同则生成不同的 Etag，再次请求时会带有 if-none-match 字段，值为上一次 Etag 的值，服务器根据这两个 Etag 进行比较，对比成功返回 304 从客户端获取，失败则返回新的 Etag 和资源。

## 原型原型链

原型：原型是 function 对象下的属性，它定义了构造函数的共同祖先，也就是一个父子级的关系，子对象会继承父对象的方法和属性
原型链：每个实例对象下都有**proto**属性，通过属性**proto**指向构造函数的原型对象，当到达末端时，返回 null，这样一层一层向顶端查找，就形成了原型链

## 事件轮询(Event Loop)

JS 运行机制就是事件循环
1):JS 分为同步任务和异步任务
2):同步任务都在主线程上执行，形成执行栈
3):主线程之外，事件触发线程管理着一个任务队列，只要异步任务有了结果，就在任务队列之中放置一个事件
4):一旦执行栈中的所有同步任务全部执行完毕（此时 JS 引擎空闲），系统会读取任务队列，将可运行的异步任务添加到可执行栈中，开始执行

## 微任务与宏任务

宏任务包括:
script（整体代码）
setTimeout
setInterval
setImmediate
I/O
UI render
微任务包括
process.nextTick（node 环境中）
Promise
Async/Await
MutationObserver（html5 新特性）
运行机制:
执行一个宏任务（栈中没有就从事件队列中获取）
执行过程中如果遇到微任务，就将它添加到微任务的任务队列中去
宏任务执行完毕后，立即依次执行当前微任务队列的所有微任务
当前宏任务执行完毕，开始检查渲染，然后 GUI 线程接管渲染
渲染完毕后，JS 引擎线程继续接管，开始下一个宏任务（从事件队列中获取）
