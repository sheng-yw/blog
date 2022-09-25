## vite
Vite是一种新型的前端构建工具，它能显著改善前端开发体验

## vite 构成
1、dev server：利用浏览器的ESM能力来提供源文件，具有丰富的内置功能并具有高效的HMR
2、生产构建：生产环境利用Rollup来构建代码，提供指令用来优化构建过程

## vite的主要特性
Instant Server Start —— 即时服务启动
Lightning Fast HMR —— 闪电般快速的热更新
Rich Features —— 丰富的功能
Optimized Build —— 经过优化的构建
Universal Plugin Interface —— 通用的Plugin接口
Fully Typed APIs —— 类型齐全的API

## vite与webpack 的区别
webpack | Vite
--- | :---:
先打包生成bundle，再启动开发服务器 | 先启动开发服务器，利用新一代浏览器的ESM能力，无需打包，直接请求所需模块并实时编译
HMR时需要把改动模块及相关依赖全部编译 | HMR时只需让浏览器重新请求该模块，同时利用浏览器的缓存（源码模块协商缓存，依赖模块强缓存）来优化请求
内存高效利用 | -

## vite原理
Vite是基于ESM，ESM是浏览器支持的一种模块化方案，允许在浏览器实现模块化。ESM的对外接口只是一种静态定义，为编译时加载，遇到模块加载命令import，就会生成一个只读引用。等脚本真正执行时，再根据这个只读引用，到被加载的那个模块内取值。由于ESM编译时就能确定模块的依赖关系，因此能够只包含要运行的代码，可以显著减少文件体积，降低浏览器压力。
Vite 对 js/ts 的处理没有使用如 glup, rollup 等传统打包工具，而是使用了 esbuild。esbuild 是一个全新的js打包工具，底层使用了go，大量使用了并行操作，可以充分利用CPU资源。esbuild支持如babel, 压缩等的功能。
Vite 的基本实现原理，就是启动一个 koa 服务器拦截由浏览器请求 ESM的请求。通过请求的路径找到目录下对应的文件做一定的处理最终以 ESM的格式返回给客户端。





