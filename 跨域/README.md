# 1.什么是跨域
    当前端请求接口时,前端的协议、域名、端口有一个与请求接口的服务器不同时,则会出现跨域,是由于浏览器的同源策略(协议、域名、端口都要相同)导致的,是为了对js的安全限制
# 2.为什么会出现跨域
    当发出请求时,浏览器会有一个校验,当校验通过时,不会引发跨域问题,反之则会触发跨域问题,校验规则为CORS规则

# 2.跨域解决方案
 ## 看服务器能否改动分为两类解决方案
  ### 能改动服务器
   (1).CORS:CORS是一套机制,用于浏览器校验跨域请求
      CORS将请求分为两种
       1.简单请求
        (1).请求方法为 get,head,post
        (2).头部字段满足CORS安全规范(不要改动请求头部就满足)
        (3).请求头的content-type为
          text/plain
          multipart/form-data
          application/x-www-form-urlencoded
       2.预检请求
        除了简单请求的请求,意思是第一次请求不是真正的请求,而是发送我是否可以请求,服务器返回可以请求,第二次发送真正的请求

      CORS检查为简单请求时,服务器设置响应头为Access-Control-Allow-Origin: * 意思是允许所有源访问服务器,或可以设置单独的源
      
      CORS检查为预检请求时
      ![请添加图片描述](https://img-blog.csdnimg.cn/f7b186314f9748b3b39590489a4f5b2b.png)
      发送请求的内容为:请求的源,请求的方法,请求头的改动
      设置的响应头为:响应的源(为*则可以响应所有源),允许的请求方法,允许的请求头,设置响应的时间(在这个时间内,来自与这个源的请求不在询问,直接响应)

    (2).JSONP:较为古老,原理是同源策略里面,对标签的跨域请求限制较小,将服务器的地址写在script标签里面,服务器响应一段js代码,如一个函数,响应的数据写在函数里面前端收到这串js代码并执行。

```javascript
function res(data){
console.log(data)
}
function bt(src){
const script = document.activeElement('script')
    script.src=src
    script.onload=()=>{
        script.remove()
    }
    document.body.appendChild(script)
}
document.querySelector('bt').oncilck = ()=>{
  bt(123.56.20.235:8081)
}
```
  ### 不能能改动服务器
   (1)代理服务器:原理是服务器请求服务器不存在跨域问题,跨域问题只有浏览器环境才有,前端请求代理服务器,由代理服务器转发请求,代理服务器获得响应,现在服务器是可以改动的了(代理服务器是自己人),在代理服务器上进行CORS规则操作或JSONP返回js代码操作都是可以的,从而解决了跨域问题,同时通过代理可以隐藏客户端的信息,对客户端进行了保护
    
