## props配置项

1. 功能：让组件接收外部传过来的数据  
2. 传递数据：```<Demo name="xxx"/>```
3. 接收数据：
    1. 第一种方式（只接收）：```props:['name'] ```
    2. 第二种方式（限制类型）：```props:{name:String}```
    3. 第三种方式（限制类型、限制必要性、指定默认值）：

  

        ```js

        props:{

         name:{

         type:String, //类型

         required:true, //必要性

         default:'老王' //默认值

         }

        }

        ```
#### props主要是父级向子级传递属性，值
- **第一步以属性的方式把要传的属性名和属性值写到对应的组件标签上**
```html
<div>

        <Student name="李四" sex="女" :age="18"/>

 </div>
```
- **第二部在子级用prop属性进行接收，这里有两种方式，数组方式是简写**
```js
<template>

    <div>

        <h1>{{msg}}</h1>

        <h2>学生姓名：{{name}}</h2>

        <h2>学生性别：{{sex}}</h2>

        <h2>学生年龄：{{myAge+1}}</h2>

        <button @click="updateAge">尝试修改收到的年龄</button>

    </div>

</template>

  

<script>

    export default {

        name:'Student',

        data() {

            console.log(this)

            return {

                msg:'我是一个尚硅谷的学生',

                myAge:this.age

            }

        },

        methods: {

            updateAge(){

                this.myAge++

            }

        },

        //简单声明接收

        // props:['name','age','sex']

  

        //接收的同时对数据进行类型限制

        /* props:{

            name:String,

            age:Number,

            sex:String

        } */

  

        //接收的同时对数据：进行类型限制+默认值的指定+必要性的限制

        props:{

            name:{

                type:String, //name的类型是字符串

                required:true, //name是必要的

            },

            age:{

                type:Number,

                default:99 //默认值

            },

            sex:{

                type:String,

                required:true

            }

        }

    }

</script>
```
![[props.1.png]]
- 这样就可以看出其实传个对象也是小问题
- 主要是这个属性是只读的，不能直接改，虽然v-model可以，因为他是浅监视，但不推荐这样
> 备注：props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据。
>