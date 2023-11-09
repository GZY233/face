 <!-- 真实dom -->
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <title>真实Dom</title>
</head>
<body>
    <h1 class="a" style="color: red;">真实dom</h1>
    <a href="123.56.20.235:8081">真实dom</a>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
</body>
</html>
```
 <!-- 虚拟dom -->
```javascript
{
 {
    tag:'h1',
    props:{class:'a',style:"color: red"},
    children:{'真实dom'}
 },
 {
    tag:'a',
    props:{href:"123.56.20.235:8081"},
    children:{'真实dom'},
 },
 {
    tag:'ul',
    props:{},
    children:{
        {
            tag:li,
            props:{},
            children:{'1'}
        },
        {
            tag:li,
            props:{},
            children:{'2'}
        },
        {
            tag:li,
            props:{},
            children:{'3'}
        }
    }
 }
}
```
1. ## **什么是虚拟dom**
    个人理解为将真实don进行对象化,真实dom转为虚拟dom涉及模板编译原理

2. ## **为什么要使用虚拟dom**
    （1）框架设计层面:因为如vue是基于数据驱动理念设计的,数据改变，视图也要变化,没有虚拟dom,就要重新渲染一遍页面,尽管只有一个数据发生变化,如果数据较多,页面复杂,这样操作真实dom会影响效率,为了缓解效率,所以引入了虚拟dom,只会改变数据改变的元素,反映到真实dom上
    
    （2）跨平台层面:虚拟dom不依赖于浏览器环境,虚拟dom是一个js对象,其他环境能够识别,可以导入相关的虚拟dom的库，可以提高效率和性能

**diff算法是在虚拟dom上面进行的,真实dom每一次变化,转化为虚拟dom与老虚拟dom进行diff(精细化比较),算出最小量更新,最后反映到真实dom上,vue里面为patch函数(新的虚拟DOM树与旧的虚拟DOM树进行比较)就是diff算法**
