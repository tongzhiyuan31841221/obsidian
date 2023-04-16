#### plugins的使用
```js
export default {

    install(Vue,x,y,z){

        console.log(x,y,z)

        **//全局过滤器**

        Vue.filter('mySlice',function(value){

            return value.slice(0,4)

        })

  

        **//定义全局指令**

        Vue.directive('fbind',{

            //指令与元素成功绑定时（一上来）

            bind(element,binding){

                element.value = binding.value

            },

            //指令所在元素被插入页面时

            inserted(element,binding){

                element.focus()

            },

            //指令所在的模板被重新解析时

            update(element,binding){

                element.value = binding.value

            }

        })

  

        **//定义混入**

        Vue.mixin({

            data() {

                return {

                    x:100,

                    y:200

                }

            },

        })

  

        **//给Vue原型上添加一个方法（vm和vc就都能用了）**

        Vue.prototype.hello = ()=>{alert('你好啊')}

    }

}
```
 
 定义插件：

  

    ```js

    对象.install = function (Vue, options) {

        // 1. 添加全局过滤器

        Vue.filter(....)

        // 2. 添加全局指令

        Vue.directive(....)

        // 3. 配置全局混入(合)

        Vue.mixin(....)

        // 4. 添加实例方法

        Vue.prototype.$myMethod = function () {...}

        Vue.prototype.$myProperty = xxxx

    }

    ```

  

4. 使用插件：```Vue.use()```
