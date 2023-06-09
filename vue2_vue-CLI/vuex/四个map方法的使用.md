### 四个map方法的使用


1. <strong>mapState方法：</strong>用于帮助我们映射```state```中的数据为计算属性，不用直接写```$store.getters.big```
   ```js

   computed: {

       //借助mapState生成计算属性：sum、school、subject（对象写法）

        ...mapState({sum:'sum',school:'school',subject:'subject'}),

       //借助mapState生成计算属性：sum、school、subject（数组写法）

       ...mapState(['sum','school','subject']),

   },

   ```

  

2. <strong>mapGetters方法：</strong>用于帮助我们映射```getters```中的数据为计算属性

  

   ```js

   computed: {

       //借助mapGetters生成计算属性：bigSum（对象写法）

       ...mapGetters({bigSum:'bigSum'}),

       //借助mapGetters生成计算属性：bigSum（数组写法）

       ...mapGetters(['bigSum'])

   },

   ```

  

3. <strong>mapActions方法：</strong>用于帮助我们生成与```actions```对话的方法，即：包含```$store.dispatch(xxx)```的函数

  

   ```js

   methods:{

       //靠mapActions生成：incrementOdd、incrementWait（对象形式）

       ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})

       //靠mapActions生成：incrementOdd、incrementWait（数组形式）

       ...mapActions(['jiaOdd','jiaWait'])

   }

   ```

  

4. <strong>mapMutations方法：</strong>用于帮助我们生成与```mutations```对话的方法，即：包含```$store.commit(xxx)```的函数

  

   ```js

   methods:{

       //靠mapActions生成：increment、decrement（对象形式）

       ...mapMutations({increment:'JIA',decrement:'JIAN'}),

       //靠mapMutations生成：JIA、JIAN（对象形式）

       ...mapMutations(['JIA','JIAN']),

   }

   ```

  

> 备注：mapActions与mapMutations使用时，若需要传递参数需要：在模板中绑定事件时传递好参数，否则参数是事件对象。