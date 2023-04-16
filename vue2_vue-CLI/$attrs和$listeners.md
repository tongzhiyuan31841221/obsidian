```vue
<template>

  <div class="container">

    <h2>自定义带hover提示的按钮</h2>

    <One

      @changeTitle="changeTitle"

      :title="title"

      type="danger"

      icon="el-icon-phone"

      size="mini"

    ></One>

  </div>

</template>


<script>

import One from "./components/One.vue";

import Two from "./components/Two.vue";

export default {
  name: "App",
  components: {
    Two,
    One,
  },
  data() {

    return {

      title: "警告",

    };

  },

  methods: {

    changeTitle(value) {

      alert(123)

    },

  },

};

</script>
```

```vue 
<template>
  <div>

    <!-- $attr回收即所有没有被props接收的数据,并可以一键绑定,到某一元素上,所以我们可以单列的采用props,其余直接一键绑定-->

    <a :title="title">
    
      <el-button v-bind="$attrs" v-on="$listeners"></el-button>
      
    </a>

  </div>

</template>

  

<script>

export default {

  name: "One",

  props: ["title"],

  mounted() {

    console.log(this.$attrs);

    console.log(this.$listeners);

    // $listeners不好用,可能是我打开方式不对,你父组件传的是个click事件才好用

  },

  methods: {},

};

</script>

  

<style>

</style>
```