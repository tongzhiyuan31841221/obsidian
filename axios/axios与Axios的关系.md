#### axios 与 Axios 的关系 ?
1.  从语法上来说: axios 不是 Axios 的实例
2.  从功能上来说: axios 是 Axios 的实例
3. axios 是 Axios.prototype.request 函数 bind()返回的函数
4.  axios 作为对象有 Axios 原型对象上的所有方法，有 Axios 对象上所有属性
```js
Axios构造函数主要是默认配置和拦截器
function Axios(instanceConfig) {

    //实例对象上的 defaults 属性为配置对象

    this.defaults = instanceConfig;

    //实例对象上有 interceptors 属性用来设置请求和响应拦截器

    this.interceptors = {

        request: new InterceptorManager(),

        response: new InterceptorManager()

    };

}
```
```js
Axios原型的request方法
/**

 * Dispatch a request

 * 发送请求的方法.  原型上配置, 则实例对象就可以调用 request 方法发送请求

 * @param {Object} config The config specific for this request (merged with this.defaults)

 */
Axios.prototype.request = function request(config) {

    /*eslint no-param-reassign:0*/

    // Allow for axios('example/url'[, config]) a la fetch API

    /**

     * axios('http://www.baidu.com', {header:{}})

     */

    if (typeof config === 'string') {

        config = arguments[1] || {};

        config.url = arguments[0];

    } else {

        config = config || {};

    }

    //将默认配置与用户调用时传入的配置进行合并

    config = mergeConfig(this.defaults, config);

  

    // Set config.method

    // 设定请求方法

    if (config.method) {

        config.method = config.method.toLowerCase();

    } else if (this.defaults.method) {

        config.method = this.defaults.method.toLowerCase();

    } else {

        config.method = 'get';

    }

  

    // Hook up interceptors middleware

    // 创建拦截器中间件  第一个参数用来发送请求, 第二个为 undefined 用来补位

    var chain = [dispatchRequest, undefined];

    // 创建一个成功的 promise 且成功的值为合并后的请求配置

    var promise = Promise.resolve(config);//  promise 成功的Promise

    // 遍历实例对象的请求拦截器,

    this.interceptors.request.forEach(function unshiftRequestInterceptors(interceptor) {

        //将请求拦截器压入数组的最前面

        chain.unshift(interceptor.fulfilled, interceptor.rejected);

    });

  

    this.interceptors.response.forEach(function pushResponseInterceptors(interceptor) {

        //将相应拦截器压入数组的最尾部

        chain.push(interceptor.fulfilled, interceptor.rejected);

    });

  

    //如果链条长度不为 0

    while (chain.length) {

        //依次取出 chain 的回调函数, 并执行

        promise = promise.then(chain.shift(), chain.shift());

    }

  

    return promise;

};
```
axios
```js
var axios = createInstance(defaults);
// axios 添加 Axios 属性, 属性值为构造函数对象  axios.CancelToken = CancelToken    new axios.Axios()
axios.Axios = Axios;
function createInstance(defaultConfig) {

    //创建一个实例对象 context 可以调用 get  post put delete request

    var context = new Axios(defaultConfig);// context 不能当函数使用  

    // 将 request 方法的 this 指向 context 并返回新函数  instance 可以用作函数使用, 且返回的是一个 promise 对象
	//bind返回是个新函数，新函数的this表掉了
    var instance = bind(Axios.prototype.request, context);// instance 与 Axios.prototype.request 代码一致
	//这个bind是自己用apply实现的
    // instance({method:'get'});  instance.get() .post()

    // Copy axios.prototype to instance

    // 将 Axios.prototype 和实例对象的方法都添加到 instance 函数身上

    utils.extend(instance, Axios.prototype, context);// instance.get instance.post ...
	//分开时因为前面要把所有的方法的this，重新绑成context
    // instance()  instance.get()

    // 将实例对象的方法和属性扩展到 instance 函数身上

    utils.extend(instance, context);

  

    return instance;

}
```
总结一下，首先第一步是重新修改Axios.prototype.request的this,实例Axios的实例，返回一个新的request函数
然后将Axios.prototype的原型对象上的东西全都搬到innstance上
#### axios与instance的区别
很简单：instance是createInstance（）的返回结果，但是我们又给axios添加了其他的属性，而且axios.create()返回的也是一样的
>![[Pasted image 20230222205513.png]]
- 相同点
	1. 都是一个能发任意请求的函数：request（）大家都是新返回的request（），this指向了Axios的实例对象
	2. 都有能发送特定请求的方法get、post。delete。。。
	3. 都有default和interceptors
		![[Pasted image 20230222210740.png]]
- 不同点
	1. default很有可能不同，两个config不同
	2. 没有后面主动添的方法
#### axios运行的整体流程
![[尚硅谷_axios从入门到源码分析 1.pdf]]
