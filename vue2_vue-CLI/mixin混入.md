#### 采用分别暴露的方式写一个mixin.js
```js
//定义混入的对象
export const hunhe = {

    methods: {
//方法也可以混入
        showName(){

            alert(this.name)

        }

    },

    mounted() {

        console.log('你好啊！')

    },

}

export const hunhe2 = {

    data() {

        return {

            x:100,

            y:200

        }

    },

}
```
#### 你要在哪用就在那里引入
```vue
<template>

    <div>

        <h2 @click="showName">学校名称：{{name}}</h2>

        <h2>学校地址：{{address}}</h2>

    </div>

</template>

  

<script>

    //引入混入的对象

    import {hunhe,hunhe2} from '../mixin'

  

    export default {

        name:'School',

        data() {

            return {

                name:'尚硅谷',

                address:'北京',

                x:666

            }

        },
//使用混入的对象
        mixins:[hunhe,hunhe2],

    }

</script>
```
![[mixin.1.png]]
- mixin混入的属性如果有重复还是以原来的为准,不重复的话就直接添加了
![[mixin.2.png]]
