
## HTTP简介
HTTP 协议是Hyper Text Transfer Protocol（超文本传输协议）的缩写,是用于从万维网（WWW:World Wide Web ）服务器传输超文本到本地浏览器的传送协议；
HTTP 是一个基于TCP/IP通信协议来传递数据（HTML文件、图片文件、查询结果等）；

## http和https有什么区别
1): https有ca证书，http一般没有；
2): http是超文本传输协议，信息是明文传输。https则是具有安全性的ssl加密传输协议；
3): http默认80端口，https默认443端口。

## HTTP协议特点
1): http无连接：限制每次连接只处理一个请求，服务端完成客户端的请求后，即断开连接。（传输速度快，减少不必要的连接，但也意味着每一次访问都要建立一次连接，效率降低）
2): http无状态：对于事务处理没有记忆能力。每一次请求都是独立的，不记录客户端任何行为
3): 客户端/服务端模型：客户端支持web浏览器或其他任何客户端
4): 简单快速
5): 灵活：可以传输任何类型的数据。

## GET和POST的区别
简单来说：GET产生一个TCP数据包，POST产生两个TCP数据包。严格的说：对于GET方式的请求，游览器会把http header和data一并发送出去，服务器响应200（返回数据）；而对于POST请求。游览器先发送header，服务器响应100continue，游览器再发送data，服务器响应200 ok（返回数据）

## http常用code解读

200 OK(成功)   PUT, DELETE, 和 OPTIONS 方法永远不会返回 200            
304 Not Modified(未修改)  告诉客户端,所请求的内容距离上次访问并没有变化. 客户端可以直接从浏览器缓存里获取该资源.    
307 Temporary Redirect(临时重定向)   
308 Permanent Redirect(永久重定向)  
400 Bad Request(错误请求)  因发送的请求语法错误,服务器无法正常读取
403 Forbidden(禁止访问) 客户端没有权利访问所请求内容,服务器拒绝本次请求.
404 Not Found(未找到) 服务器找不到所请求的资源.由于经常发生此种情况,所以该状态码在上网时是非常常见的
405 Method Not Allowed(不允许使用该方法) 
408 Request Timeout(请求超时)    
500 Internal Server Error(内部服务器错误)   
502 Bad Gateway(网关错误)    
504 Gateway Timeout (网关超时)     

## http 请求响应结构
请求：
1、请求行：请求方法，请求url，http版本
2、请求头：关键字/值对组成，每行一对
3、换行
4、请求体

响应：
1、状态行：协议版本、状态码、原因短语
2、消息报头
3、空行
4、响应正文




