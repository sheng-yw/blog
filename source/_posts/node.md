# egg框架

## egg之框架统一错误处理
  config/default.config.js 中配置
  `config.onerror = {`
  `  all: (err, ctx) => {`
  `    ctx.set({'Content-Type': 'application/json'});`
  `    ctx.status = 200;`
  `    ctx.body = JSON.stringfy({`
  `      success: false,`
  `      message: err.message`
  `    })`
  `  }`
  `}`
## pm2相关
  pm2 list 查看启动的服务
  pm2 stop ip 停止某一个服务
  pm2 start pm2.json 在项目目录下 pm2 启动某一个项目
  pm2 delete ip 删除某一个服务
  pm2 restart ip 重启某个服务
  pm2 log ip 查看某一个服务的日志
  pm2 启动时指定node版本需要在pm2.json中配置 "interpreter": "./node_modules/.bin/node",
  或者在执行 pm2 start server.js --interpreter ./node_modules/.bin/node
## avn相关
  avn 是一个自动切换node版本的管理工具，需要和nvm配合使用 npm i avn avn-nvm -g
  需要在项目中配置.node-version文件 内容例如：12.0.0
  cd 到当前目录中会自动切换到这个版本的node

## nodeinstall相关
  nodeinstall 可以使node服务采用node_modules中的node 依赖而不依赖后端
  npm i nodeinstall -g 
  安装完自身依赖以后执行 nodeinstall 10.0.0 
  查看安装版本 ./node_modules/.bin/node -v
## 爬虫下载的图片打不开 错误信息download token not specified
  检查发现把url后面参数给截取了
## puppetter 包部署问题
1、Chrome reversion is not downloaded
打包发现没有安装linux版本相关的chromu插件 需要手动安装 node ./node-modules/puppetter/install.js
2、Failed to launch the browser process! spawn
是因为linux服务缺少chromu相关插件，根据git相关问答提示进行安装相关依赖
实例化chromu时添加参数
await puppeteer.launch({
  headless: true, 
  args: ['--no-sandbox', '--disable-setuid-sandbox'],
  executablePath: '/opt/conf/chrome/chrome-linux/chrome'
})

