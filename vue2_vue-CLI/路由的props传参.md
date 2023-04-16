### 路由的props配置

  
​  作用：让路由组件更方便的收到参数
 - 其实你用props传参就算组件那边你用params，其实也不用站位  

```js

{

   name:'xiangqing',

   path:'detail/:id',

   component:Detail,

  

   //第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件

   // props:{a:900}只能写死数据，不怎么用

  

   //第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件

   // props:true

   //第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件，可以定义query，params

   props(route){

      return {

         id:route.query.id,

         title:route.query.title

      }

   }

}
```
