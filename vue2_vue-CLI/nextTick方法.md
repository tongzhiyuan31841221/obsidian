## nextTick


1. 语法：```this.$nextTick(回调函数)```

2. 作用：在下一次 DOM 更新结束后执行其指定的回调。

3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。
4. 有种等效的方法settimeout(()=>{},)不设定时间，由于定时器的执行机制，会进入异步队列，不会立即执行
#### 就是为了解决这个问题
```js
    editTodo(e) {

      this.todo.isedit = true;

      // 由于vue会等你整个方法执行完毕在重新解析模板，所以执行focus的时候DOM都没出来所以我们是用nextick

       this.$nextTick(function(){

        this.$refs.edtingbox.focus()

      });

      this.text=this.todo.title

      this.todo.title=""

    },
```