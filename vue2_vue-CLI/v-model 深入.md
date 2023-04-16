## v-model基本使用:双向数据绑定
感觉只对表单好使
<!DOCTYPE html>
```html
<html>
        <head>
                <meta charset="UTF-8" />
                <title>数据绑定</title>
                <!-- 引入Vue -->
                <script type="text/javascript" src="../js/vue.js"></script>
        </head>
<body>
                <!--
		Vue中有2种数据绑定的方式：

			1.单向绑定(v-bind)：数据只能从data流向页面。
	
			2.双向绑定(v-model)：数据不仅能从data流向页面，还可以从页面流向data。

		备注：

			1.双向绑定一般都应用在表单类元素上（如：input、select等）
	
			2.v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。

                 -->

                <!-- 准备好一个容器-->

<div id="root">

	<!-- 普通写法 -->

	<!-- 单向数据绑定：<input type="text" v-bind:value="name"><br/>

	双向数据绑定：<input type="text" v-model:value="name"><br/> -->

	<!-- 简写 -->

	单向数据绑定：<input type="text" :value="name"><br/>

	双向数据绑定：<input type="text" v-model="name"><br/>

	<!-- 如下代码是错误的，因为v-model只能应用在表单类元素（输入类元素）上 -->

	<!-- <h2 v-model:x="name">你好啊</h2> -->

</div>

</body>

<script type="text/javascript">

	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({

			el:'#root',

			data:{

					name:'尚硅谷'

			}

	})

</script>

</html>
```
## v-model的一点小技巧
<font color="#953734">见OneNote</font>
## v-model其实也是一种通信方式-可以实现父子数据互通
```vue
<template>
  <div class="container">

    <h2>我是APP组件</h2>

    <input type="text" v-model="msg" />

    <!--

      首先我们用props给One传一个value属性,值是msg

      然后崽子组件中,我们可以使用bind,这样父传子就实现了

      然后给One设置自定义事件input,接受自组件的value,完成子传父

     -->

    <One :value="msg" @input="sendmsg"></One>

    <!-- 这就是简写 -->

    <One v-model="msg"></One>

  </div>

</template>


<script>

import One from "./components/One.vue";

import Two from "./components/Two.vue";

export default {
  name: "App",
  data() {
    return {
      msg: "",
    };
  },
  components: {
    Two,
    One,
  },
  methods: {
    sendmsg(val) {
      this.msg = val;
    },
  },
};
</script>

``` vue
<template>
  <div>
    <h2 @click="emitevent2">我是One组件</h2>
    <label for="first">
      <input
        name="first"
        type="text"
        :value="value"
        @input="$emit('input', $event.target.value)"
    /></label>
  </div>
</template>
  
<script>
export default {
  name: "One",
  props: ["value"],
};
</script>

```