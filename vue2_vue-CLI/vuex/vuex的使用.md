首先是一种组建通信方式
  

## Vuex

### 1.概念

​     在Vue中实现集中式状态（数据）管理的一个Vue插件，对vue应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。
  

### 2.何时使用？
  
​     多个组件需要共享数据时

### 3.搭建vuex环境

1. 创建文件：```src/store/index.js```
  

   ```js

   //引入Vue核心库

   import Vue from 'vue'

   //引入Vuex

   import Vuex from 'vuex'

   //应用Vuex插件,这里要先有vuex才能实例化store，vue对于导入模块有一种声明提升的感觉

   Vue.use(Vuex)

   //准备actions对象——响应组件中用户的动作

   const actions = {}

   //准备mutations对象——修改state中的数据

   const mutations = {}

   //准备state对象——保存具体的数据

   const state = {}

   //创建并暴露store

   export default new Vuex.Store({

      actions,

      mutations,

      state

   })

   ```

  

2. 在```main.js```中创建vm时传入```store```配置项

  

   ```js

   ......

   //引入store

   import store from './store'

   ......

   //创建vm

   new Vue({

      el:'#app',

      render: h => h(App),

      store

   })

   ```

  

###    4.基本使用

  

1. 初始化数据、配置```actions```、配置```mutations```，操作文件```store.js```

  

   ```js

   //引入Vue核心库

   import Vue from 'vue'

   //引入Vuex

   import Vuex from 'vuex'

   //引用Vuex

   Vue.use(Vuex)

   const actions = {

       //响应组件中加的动作

      jia(context,value){

         // console.log('actions中的jia被调用了',miniStore,value)

         context.commit('JIA',value)

      },

   }

   const mutations = {

       //执行加

      JIA(state,value){

         // console.log('mutations中的JIA被调用了',state,value)

         state.sum += value

      }

   }

   //初始化数据

   const state = {

      sum:0

   }

   //创建并暴露store

   export default new Vuex.Store({

      actions,

      mutations,

      state,

   })

   ```

  

2. 组件中读取vuex中的数据：```$store.state.sum```

  

3. 组件中修改vuex中的数据：```$store.dispatch('action中的方法名',数据)``` 或 ```$store.commit('mutations中的方法名',数据)```

  

   >  备注：若没有网络请求或其他业务逻辑，组件中也可以越过actions，即不写```dispatch```，直接编写```commit```

  

### 5.getters的使用

  

1. 概念：当state中的数据需要经过加工后再使用时，可以使用getters加工。
   相当于vuex自己的计算属性
  

2. 在```store.js```中追加```getters```配置

  

   ```js

   ......

   const getters = {

      bigSum(state){

         return state.sum * 10

      }

   }

   //创建并暴露store

   export default new Vuex.Store({

      ......

      getters

   })

   ```

  

3. 组件中读取数据：```$store.getters.bigSum```
4. 实例 
```js
import Vue from "vue"

import Vuex from "vuex"

// 使用vuex

Vue.use(Vuex)

// 该文件用于创建store

// 用于响应组建的动作

// 业务逻辑的封装放在这里

const actions = {

    increment(context, value) {

        // console.log(context,value)

        // context.state.sum+=value极其不推荐

        console.log(context, value)

        context.commit("Increment", value)

    },

    decrement(context, value) {

        context.commit("Decrement", value)

    },

    incrementOdd(context, value) {

        if (value % 2 == 0) return

        context.commit("IncrementOdd", value)

    },

    incrementWait(context, value) {

        setTimeout(() => {

            context.commit("IncrementWait", value)

        }, 1000);

    },

    addperson(context,value){

        context.commit("AddPerson",value)

    }

}

// 用于操作数据（state）

const mutations = {

    Increment(state, value) {

        // console.log(state,value)

        state.sum += value

    },

    Decrement(state, value) {

        state.sum -= value

    },

    IncrementOdd(state, value) {

        if (value % 2 == 0) return

        state.sum += value

    },

    IncrementWait(state, value) {

        state.sum += value

    },

    AddPerson(state,value){

        console.log("添加成功")

        state.personList.push(value)

    }

}

// 数据

const state = {

    sum: 0,

    personList: [{

        id: "001", name: "zhangsan1", sex: "男"

    },  {

        id: "002", name: "zhangsan2", sex: "男"

    }, {

        id: "003", name: "zhangsan3", sex: "男"

    }, {

        id: "004", name: "zhangsan4", sex: "男"

    }]

}

  

// const store =Vuex.store({

//     actions,

//     mutations,

//     state,

// })

// export default state

export default new Vuex.Store({

    actions,

    mutations,

    state,

})
```
#### 注意点
1. increment，和decrement这种在actions中啥事都没干，直接调用了commit，其实在actions中可以省略，在组件中可以直接调用commit
```js
increment() {

      this.$store.commit("Increment",this.n)

    },

    decrement() {

      this.$store.commit("Decrement",this.n)

    },
```
2. 异步请求，业务逻辑可以放在actions中，注意过于复杂的业务逻辑，可通过dispatch调用其他的函数进行进一步处理
3. getters的配置方法，方法只接收一个参数那就是state，**通过返回值进行操作，千万别忘了**






