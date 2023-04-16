```vue
<template>

  <div class="container">

    <h2>我是APP组件,我有{{ money }}元</h2>

    <h2>sync修饰符</h2>

    <!-- @update:money="money = $event",

    这是一种简写方式 .直接把$emit("xxx",a,b)的第一个参数赋值给money,
    其余参数被忽略,有点像prop的双向绑定,当你子元素影响父级时有点好用,如果操作复杂$emit()那里可以放个函数来返回-->

    <One :money="money" @update:money="money=$event"></One>

    <Two :money.sync="money"></Two>

  </div>

</template>

<script>
import One from "./components/One.vue";

import Two from "./components/Two.vue";

export default {

  name: "App",

  data() {

    return {

      money: 10000,

    };

  },

  components: {

    Two,

    One,

  },

  methods: {

    updateMoney(currentmoney) {

      this.money =currentmoney;

    },

  },

};

</script>

<style>

* {

  margin: 20px;

}

  

</style>
```

```vue
<template>

  <div>

    <h2>我是One组件</h2>

    <!-- 就是把变化后的钱传回去 -->

    <button @click="$emit(`update:money`, huaqian(100), )">

      儿子向父亲借了50元

    </button>

    <span>父亲还剩{{ money }}</span>

  </div>

</template>  

<script>

export default {

  name: "One",

  props: ["money"],

  methods:{

    huaqian(){

      return this.money-100

    }

  }

};

</script>


<style>

</style>
```