>总共有四个api
>1.**setItem(key,value)**
>2.**getItem(key)**
>3.**removeItem("key")**
>4.**clear()**
>5.**其实还可以通过索引来拿数据**
>### 注意value只能是字符串，不是的话会自动调用tostring
>

```js
<!DOCTYPE html>

<html>

    <head>

        <meta charset="UTF-8" />

        <title>localStorage</title>

    </head>

    <body>

        <h2>localStorage</h2>

        <button onclick="saveData()">点我保存一个数据</button>

        <button onclick="readData()">点我读取一个数据</button>

        <button onclick="deleteData()">点我删除一个数据</button>

        <button onclick="deleteAllData()">点我清空一个数据</button>

  

        <script type="text/javascript" >

            let p = {name:'张三',age:18}

  

            function saveData(){

                localStorage.setItem('msg','hello!!!')

                localStorage.setItem('msg2',666)

                localStorage.setItem('person',JSON.stringify(p))

            }

            function readData(){

                console.log(localStorage.getItem('msg'))

                console.log(localStorage.getItem('msg2'))

                // 可以用keys拿到所有的

                const result = localStorage.getItem('person')

                console.log(JSON.parse(result))

  

                // console.log(localStorage.getItem('msg3'))

            }

            function deleteData(){

                localStorage.removeItem('msg2')

            }

            function deleteAllData(){

                localStorage.clear()

            }

        </script>

    </body>

</html>
```

```js
<!DOCTYPE html>

<html>

    <head>

        <meta charset="UTF-8" />

        <title>sessionStorage</title>

    </head>

    <body>

        <h2>sessionStorage</h2>

        <button onclick="saveData()">点我保存一个数据</button>

        <button onclick="readData()">点我读取一个数据</button>

        <button onclick="deleteData()">点我删除一个数据</button>

        <button onclick="deleteAllData()">点我清空一个数据</button>

  

        <script type="text/javascript" >

            let p = {name:'张三',age:18}

  

            function saveData(){

                sessionStorage.setItem('msg','hello!!!')

                sessionStorage.setItem('msg2',666)

                sessionStorage.setItem('person',JSON.stringify(p))

            }

            function readData(){

                console.log(sessionStorage.getItem('msg'))

                console.log(sessionStorage.getItem('msg2'))

  

                const result = sessionStorage.getItem('person')

                console.log(JSON.parse(result))

  

                // console.log(sessionStorage.getItem('msg3'))

            }

            function deleteData(){

                sessionStorage.removeItem('msg2')

            }

            function deleteAllData(){

                sessionStorage.clear()

            }

        </script>

    </body>

</html>
```
## webStorage

  

1. 存储内容大小一般支持5MB左右（不同浏览器可能还不一样）

  

2. 浏览器端通过 Window.sessionStorage 和 Window.localStorage 属性来实现本地存储机制。

  

3. 相关API：

  

    1. ```xxxxxStorage.setItem('key', 'value');```

                  该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。

  

    2. ```xxxxxStorage.getItem('person');```

  

        ​      该方法接受一个键名作为参数，返回键名对应的值。

  

    3. ```xxxxxStorage.removeItem('key');```

  

        ​      该方法接受一个键名作为参数，并把该键名从存储中删除。

  

    4. ``` xxxxxStorage.clear()```

  

        ​      该方法会清空存储中的所有数据。

  

4. 备注：

  

    1. SessionStorage存储的内容会随着浏览器窗口关闭而消失。

    2. LocalStorage存储的内容，需要手动清除才会消失。

    3. ```xxxxxStorage.getItem(xxx)```如果xxx对应的value获取不到，那么getItem的返回值是null。

    4. ```JSON.parse(null)```的结果依然是null。