这个属性很简单就是为了防止style冲突，让这个组件的样式只在这个组件中有效
```js
<template>

    <div class="demo">

        <h2 class="title">学校名称：{{name}}</h2>

        <h2>学校地址：{{address}}</h2>

    </div>

</template>

  

<script>

    export default {

        name:'School',

        data() {

            return {

                name:'尚硅谷atguigu',

                address:'北京',

            }

        }

    }

</script>

  

<style scoped>

    .demo{

        background-color: skyblue;

    }

</style>
```