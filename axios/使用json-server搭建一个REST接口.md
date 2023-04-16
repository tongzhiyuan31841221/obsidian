[typicode/json-server: Get a full fake REST API with zero coding in less than 30 seconds (seriously) (github.com)](https://github.com/typicode/json-server)
首先到GitHub上面去搜json-server,看他的readme
总共就三步
- 安装json-server :npm install -g json-server
- 在项目的根路径写个db.json
- json-server --watch db.json
REST api:表示请求方式决定了后台的操作方式,一个请求路径可以对应不同操作
#### get请求:参数的设定
1. query参数,会查找所有符合要求的数据,封装成一个数组 
2. params参数,直接把对应项返回出来
###### 写个减一半的axios
1. 返回值是个promise,成功失败
2. 能处理多种请求
3. params参数:GET/delete的query参数
4.  data :POST/DELETE请求的请求体参数
5. 响应JSON数据,自动转化为js   JSON.parse
#### 使用axios
```js
// 配置基本路径

        axios.defaults.baseURL = "http://localhost:3000"

        function testGet() {

            axios({

                method: "get",

                url: "/posts",

                params: {

                    id: 1

                }

            }).then(response => {

                console.log(`get`, response);

            })

        }

        function testPost() {

            axios({

                method: "post",

                url: "/posts",

                data: {

                    "title": "1111",

                    "author": "1111"

                }

            }).then(response => {

                console.log("post", response);

            })

        }

  

        function testPut() {

            axios({

                method: "put",

                // put更新的参数用params 放到路径后面,具体更新成什么用data,请求体参数

                url: "/posts/1",

                data: {

                    "title": "2222",

                    "author": "2222"

                }

            }).then(response => {

                console.log("put", response)

  

            })

        }

        function testDelete() {

            axios({

                method: "delete",

                url: `posts/1`

            }).then(response => {

                console.log("delete", response)

            })

        }
```

```js
 function testGet(id){

        axios.get(`http://localhost:3000/posts?id=${id}`)

        .then((res=>{

            console.log("get",res.data);

        }))

    }

    function testPost(){

        axios.post(`http://localhost:3000/posts`,{ "id": 30, "title": "json-server30", "author": "typicode30" })

        .then((res=>{

            console.log("post",res.data);

        }))

    }

    function testPut(){

        axios.put("http://localhost:3000/posts/1",{"title": "json-....", "author": "typicode30" })

        .then(value=>{

            console.log(value.data);

        })

    }  

    function testDelete(id=30){

        axios.get(`http://localhost:3000/posts?id=${id}`)

        .then((res=>{

            console.log("del",res.data);

        }))

    }
```