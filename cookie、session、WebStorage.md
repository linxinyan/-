一、cookie和session

cookie和session都是用来跟踪浏览器用户身份的会话方式。

区别：

1、保持状态：cookie保存在浏览器端，session保存在服务器端

2、工作原理
 cookie工作原理
 
（1）客户端第一次请求服务器，服务器创建cookie对象，然后将该Cookie发送到客户端。

（2）客户端再次访问服务器端时会携带服务端创建的Cookie

（3）服务器端通过Cookie中携带的数据区分不同的用户

 session工作原理
 
（1）客户端第一次发送请求到服务端，服务端创建一个Session，同时会创建一个特殊的Cookie（name为JSESSIONID的固定值，value为session对象的ID），然后将该Cookie发送至浏览器端

（2）客户端再次发送请求到服务端,客户端就会携带该特殊Cookie对象

（3）服务端根据sessionId,去查询Session对象，从而区分不同用户。

3、存储内容：cookie只能保存字符串类型；session能支持任何类型的对象(session中可含有多个对象)

4、存储的大小：cookie：单个cookie保存的数据不能超过4kb（有个数限制（各浏览器不同），一般不能超过20个。）；session大小没有限制。

5、安全性：Cookie有安全隐患，通过拦截或本地文件找得到你的cookie后可以进行攻击；session的安全性大于cookie。

    原因如下：
    （1）sessionID存储在cookie中，若要攻破session首先要攻破cookie；
    （2）sessionID是要有人登录，或者启动session_start才会有，所以攻破cookie也不一定能得到sessionID；
    （3）第二次启动session_start后，前一次的sessionID就是失效了，session过期后，sessionID也随之失效。
    （4）sessionID是加密的　　　　　　　　
6、缺点：
        
cookie：大小受限、安全性较低，每次访问都要传送cookie给服务器，浪费带宽。

session：

（1）Session保存的东西越多，就越占用服务器内存，对于用户在线人数较多的网站，服务器的内存压力会比较大。
     
（2）依赖于cookie（sessionID保存在cookie），如果禁用cookie，则要使用URL重写，不安全     

Web Storage存储机制是对HTML4中cookie存储机制的一个改善。

HTML5的WebStorage提供了两种API：localStorage（本地存储）和sessionStorage（会话存储）。

1、生命周期：

localStorage:localStorage的生命周期是永久的，关闭页面或浏览器之后localStorage中的数据也不会消失。localStorage除非主动删除数据，否则数据永远不会消失。

sessionStorage的生命周期是在仅在当前会话下有效。sessionStorage引入了一个“浏览器窗口”的概念，sessionStorage是在同源的窗口中始终存在的数据。只要这个浏览器窗口没有关闭，即使刷新页面或者进入同源另一个页面，数据依然存在。但是sessionStorage在关闭了浏览器窗口后就会被销毁。同时独立的打开同一个窗口同一个页面，sessionStorage也是不一样的。

2、存储大小：localStorage和sessionStorage的存储数据大小一般都是：5MB

3、存储位置：localStorage和sessionStorage都保存在客户端，不与服务器进行交互通信。

4、存储内容类型：localStorage和sessionStorage只能存储字符串类型，对于复杂的对象可以使用ECMAScript提供的JSON对象的stringify和parse来处理

5、获取方式：localStorage：window.localStorage;；sessionStorage：window.sessionStorage;。

6、应用场景：localStoragese：常用于长期登录（+判断用户是否已登录），适合长期保存在本地的数据。sessionStorage：敏感账号一次性登录；

WebStorage的优点：

（1）存储空间更大：cookie为4KB，而WebStorage是5MB；

（2）节省网络流量：WebStorage不会传送到服务器，存储在本地的数据可以直接获取，也不会像cookie一样美词请求都会传送到服务器，所以减少了客户端和服务器端的交互，节省了网络流量；

（3）对于那种只需要在用户浏览一组页面期间保存而关闭浏览器后就可以丢弃的数据，sessionStorage会非常方便；

（4）快速显示：有的数据存储在WebStorage上，再加上浏览器本身的缓存。获取数据时可以从本地获取会比从服务器端获取快得多，所以速度更快；

（5）安全性：WebStorage不会随着HTTP header发送到服务器端，所以安全性相对于cookie来说比较高一些，不会担心截获，但是仍然存在伪造问题；

（6）WebStorage提供了一些方法，数据操作比cookie方便；

    setItem (key, value) ——  保存数据，以键值对的方式储存信息。
    getItem (key) ——  获取数据，将键值传入，即可获取到对应的value值。
    removeItem (key) ——  删除单个数据，根据键值移除对应的信息。
    clear () ——  删除所有的数据
    key (index) —— 获取某个索引的key
