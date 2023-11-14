## 1.什么是promise(承诺)
 **promise是一个构造函数,由ES6引入,原生js即可使用,不依赖任何库,通过promise构造函数可以new一个promise实例对象,具有promise构造函数的属性和方法**

## 2.promise解决了什么问题
 **在promise没有出现的时候,解决异步方案是通过回调函数解决的如下，形成了一个回调地狱,promise的出现解决了回调地狱的问题(代码可读性差,维护差,性能差,不便于错误处理),promise支持链式(then)调用,也解决了代码可读性的问题**
```javascript
//回调地狱
setTimeout(()=>{
    console.log(1)
    setTimeout(()=>{
      console.log(2)
      setTimeout(()=>{
        console.log(3)
      },1000)
    },1000)
},2000)
```

## 3.promise的核心功能、方法
 ### 核心功能
```javascript
//promise构造函数里面接收一个函数,函数里面包裹一个异步操作
//接收两个参数,都为函数类型,resolve(解决,异步任务成功时会调用resolve),reject(拒绝,异步任务失败的时候调用reject)
const pro = new promise((resolve,reject)=>{
     setTimeout(()=>{
       //产生一个0--100随机整数,floor向下取整
       let num = Math.floor(Math.random()*100)
       if(num<30){
        //可以携带参数由then回调函数形参接收
        //成功时会将promise对象状态由pending(进行中)变为fulfilled
        resolve(num) 
       }
       else{
         //失败时会将promise对象状态由pending(进行中)变为rejected
        reject(num)
       }
     },2000)
})
//调用then回调函数,第一个函数为成功状态的回调,第二个函数为失败状态的回调
pro.then((value)=>{
 console.log(num);
 //返回一个字符串,数字,null,false等非promise对象会将promise对象状态由pending(进行中)变为fulfilled,返回promise对象的话,看promise的返回状态
 return 'num是小于30的哦'
},(reason)=>{
 console.log(num)
 //抛出错误
 throw 'num是大于30的哦'
}).then((value)=>{ //采用了then链式调用,回调的函数由上一个then回调的返回结果状态绝定
  console.log(value) //num是小于30的哦
},(reason)=>{
  console.log(reason) //报错,信息为num是大于30的哦
}
)
```