## vue是一个渐进式的框架:所谓渐进式框架是从底向上的,可以只使用vue框架,也可以往框架里面每个层面分别写入vuex、vue-router、elementyi等

vue分为以下几层
declarative rendering（声明式渲染）声明数据,渲染模板
component system（组件系统）可以写入不同设计的组件
client-side routing（前端路由）如vue-router,自己写的路由
state management（状态管理）如vuex,pinia等
build system（构建系统） 可以通过webpack以及其他构建工具搭建项目,也可以用vue-cli

每层都是可选的,根据不同需求进行定制,是为渐进式