# Nginx
1、安装
  1)、上传tgz压缩包至服务器
  2)、tar -zxvf nginx.tgz
  3)、执行 ./configure --prefix=自定义目录
  4)、make && make install
  5)、cd 自定义目录
  6)、启动 ./sbin/nginx
  7)、重启 ./sbin/nginx -s reload
2、查看ng进程
  ps –ef | grep 
3、查看ng服务
  ps -A | grep nginx    
# 配置
ng文件包括1、全局模块；2、http模块；3、events模块
http模块嵌套多个server,配置代理,缓存,日志等
server模块配置虚拟主机的相关参数，一个http中可以配置多个server
server中location块是处理符合请求规则的资源导向问题，也是我们主要配置的核心模块
loaction中匹配规则
location = /uri =开头表示精确匹配，只有完全匹配上才能生效
lcoation = ^ ~/uri ^~ 开头对URL路径进行前缀匹配，并且在正则之前
location ~ pattern 　~开头表示区分大小写的正则匹配。
location ~* pattern 　~*开头表示不区分大小写的正则匹配。
location /uri 不带任何修饰符，也表示前缀匹配，但是在正则匹配之后。
location / 　通用匹配，任何未匹配到其它location的请求都会匹配到，相当于switch中的default
location 与 root相结合表示的是实际请求的资源会自动拼接location后的uri
location 与 alias相结合表示的是实际请求的资源会去alias配置的路径去获取 但是后缀要加"/"


 
# 负载均衡

