# 跨域

## 什么是跨域，为什么要跨域

## 哪些情况会产生跨域问题

## 跨域的解决方案

## 常见问题

### The 'Access-Control-Allow-Origin' header contains multiple values 'http://eacc.chamc.com.cn,http://10.128.32.140', but only one is allowed.

服务器端设置响应Header，Access-Control-Allow-Origin为多个域名，客户端的Ajax请求配置了withCredentials为true。
然而withCredentials必须设置为true:
不同域下的XmlHttpRequest 响应，不论其Access-Control- header 设置什么值，都无法为它自身站点设置cookie值，除非它在请求之前将withCredentials 设为true。
参考：
https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/Errors/CORSNotSupportingCredentials
https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/withCredentials
