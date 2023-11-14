**AjAX是为async javascript and XMl(异步JavaScript和XML),是一种技术,不依赖于任何库,原生js可以使用与服务器进行交互**
### get请求
```javascript
// 通过构造函数创建xhr对象
const xhr = new XMLHttpRequest()
// 初始化xhr
xhr.open('get',"123.56.20.235:8081/list")
//设置请求头,如果没有需求,无需改动
xhr.setRequestHeader('','')
// 发送请求
xhr.send()
//绑定事件,处理响应
xhr.onreadystatechange = function(){
// readystate是xhr对象的属性表示状态0(未初始化),1(初始化完成),2(发送亲求完成),3(返回部分响应结果),4(返回全部响应结果)
 if(xhr.readystate===4){
 //判断响应状态码 2xx为成功响应状态码
  if(xhr.state>=200 && xhr.state<300){
  //处理响应结果
   console.log(xhr.state) //返回的状态码
   console.log(xhr.stateText) //状态字符串
   console.log(xhr.getAllResponseHeaders()) //返回所有响应头
   console.log(xhr.response) //返回响应体

  }
 }
}
```
### post请求
```javascript
xhr.send() //在send里面设置请求体
```