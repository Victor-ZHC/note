# 阿里巴巴前端
1. JS是单线程的，异步的
* JS是单线程的，浏览器只分配给js一个主线程，执行顺序是从上到下依次执行。单线程意味着本身不可能异步，但JS的宿主环境是多线程的。
2. JavaScript的异步有几种实现方式
* 法一：回调函数
```
function f1(callback) {
    setTimeout(function() {
        // f1的代码
        callback();
    }, 1000);
}
```
* 法二：事件监听
```
f1.on(‘click’, f2);
```
* 法三：发布/订阅模式
```
jQuery.subscribe(“done”, f2); // f2向信号中心jQuery订阅done信号
function f1() {
    setTimeout(function() {
        // f1的代码
        jQuery.publish(“done”);  // f1执行完成后，向信号中心jQuery发布done信号
    }, 1000);
}
```
* 法四：Promises对象
```
f1().then(f2); // f1的回调函数是f2
```
3. 回调函数callback是不是一定是异步的
* 不是，异步需要保证执行顺序，需要回调函数，两者不等价，回调函数是代码的写法  
4. NodeJS的JS实现是单线程的吗
* 是，在主线程维护一个事件队列，接到请求后，将请求作为事件放入队列中，当主线程空闲时，循环事件队列，检查队列中是否有要处理的事件（array.shift（）从队列头部拿出事件）
* Nodejs实现异步的核心是事件驱动，即：把每一个任务都当做事件处理
5. HTTP请求响应过程
```
1）域名解析
2）发起TCP的3次握手
    2.1）客户机发送SYN消息
    2.2）服务器使用SYN+ACK应答
    2.3）客户机发送ACK应答
3）建立TCP连接后发起HTTP请求
    3.1）请求行+HTTP头+内容
    3.2）请求行：请求方法（Get、Post等）
    3.3）HTTP头：如：request header
    3.4）内容：Get请求无，Post请求有
4）Web Server响应HTTP
    4.1）状态行+HTTP头+返回内容
    4.2）状态行中有状态码
    4.3）HTTP头：如：response header
    4.4）返回内容：如：Content-Type: text/html
5）浏览器解析HTML代码
    多个HTTP请求可以仅依靠一个TCP连接，即：持久连接
6）传输完成，断开，四次挥手
    6.1）客户端发送FIN报文主动关闭数据发送
    6.2）服务器端未必关闭发送数据，先响应ACK
    6.3）服务器端完成发送数据，发送FIN报文
    6.4）客户端发送ACK，一段时间后Close，服务器端接收到ACK，Close
```
6. 加载到服务器，不止一台服务器怎么处理？
* 负载均衡（也就是建立一对多的映射），如：nginx
* 不同的负载均衡技术：
    * DNS轮询
        * 以域名作为访问入口，配置多条DNS记录使得请求可以分配到不同的服务器
    * CDN（Content Delivery Network，内容分发网络）
        * 将请求内容分发到大量缓存节点，并找出离用户最近的节点
    * IP负载均衡，如：NAT
        * NAT服务器：工作在传输层，可以修改发送来的IP数据包，将数据包的目标地址修改为实际的服务器地址
    * 一致性hash
        * 求出服务器节点的哈希值，并将其配置到0～2^32的圆上。
        * 采用同样方法求出存储数据的键的哈希值，并映射到相同圆上。
        * 从数据映射到的位置开始顺时针查找，将数据保存到找到的第一个服务器上。
7. HTML的加载过程
```
1）网页发出http请求，返回HTML，网页渲染开始
   1.1）遇到link标签，又发送一次http请求，请求CSS文件
   1.2）遇到script标签，也发送http请求
2）渲染引擎对HTML解析
   2.1）把标签转化为内容树中的DOM节点，解析后构建DOM（document object model）树
   2.2）CSS解析style元素和外部文件中的样式数据，构建样式规则，样式规则和HTML中的显示控制共同创建一颗渲染树
   2.3）每个节点在屏幕上标志确切位置，该过程为：布局处理
   2.4）绘制（异步的过程）
3）javascript编译
   3.1）通过词法分析等匹配句法规则，也会创建一颗解析树
4）注：关于reflow（回流）和repaint（重绘）
   4.1）reflow回流，渲染树重新计算，回流一定会发生重绘
   4.2）repaint重绘，CSS元素更改新的属性值
```
8. DOM文档的加载顺序
```
1）DOM加载到link标签
   CSS文件的加载与DOM是并行的，构建DOM树时遇到CSS样式，会向服务器发送请求
2）DOM加载到script标签
   js文件不会与DOM并行加载，需等待js加载完再继续DOM的加载，因此，需要：$(document).ready(function(){})，让DOM文档加载完再执行js文件
```
9. CSS的样式加载顺序（优先级）
```
1）元素上的style > 文件头上的style > 外部样式文件
2）样式文件中
   2.1）id选择器指定的样式 > 类选择器指定的样式 > 元素类型指定的样式（如：h1）
   2.2）文件中越靠后优先级越高
   2.3）提高样式优先级：!important
```
10. CSS存在继承吗
* 存在，即：特定的CSS属性向下传递到子孙元素（按照HTML的DOM树）
* CSS inherit关键字，指定一个属性应从父元素继承它的值
11. IP是OSI体系结构的第几层
* 网络层
12. `==`和`===`的区别
* ==两边值类型不同时，先进行类型转换，再比较
* ===不做类型转换，严格相等
13. JS继承的几种方式
* 父类
```
// 定义一个动物类
function Animal (name) {
    // 属性
    this.name = name || 'Animal';
    // 实例方法
    this.sleep = function(){
        console.log(this.name + '正在睡觉！');
    }
}
// 原型方法
Animal.prototype.eat = function(food) {
    console.log(this.name + '正在吃：' + food);
};
```
* 1）原型链继承
    * 核心：将父类的实例作为子类的原型
```
function Cat(){ }
Cat.prototype = new Animal();
Cat.prototype.name = 'cat';
```
* 2）构造继承
    * 核心：使用父类的构造函数来增强子类实例
```
function Cat(name){
    Animal.call(this);
    this.name = name || 'Tom';
}
```
* 3）实例继承
    * 核心：为父类添加新特性，作为子类返回
```
function Cat(name){
    var instance = new Animal();
    instance.name = name || 'Tom';
    return instance;
}
```
14. JavaScript的基本数据类型和引用数据类型
* 基本数据类型：按值访问
    * Number、String、Boolean、Null和Undefined 
* 引用数据类型：保存在堆内存中的对象，不可以直接访问堆内存空间，而是要操作栈内存中的引用地址
    * Object、Array、Function、Data
15. ES6新特性（使得前后端越来越像）
https://www.cnblogs.com/Wayou/p/es6_new_features.html
* 各点的重点：
```
1）箭头操作符
2）类的支持
3）定义方法可以不用function
    breathe() {
        console.log('breathing...');
    }
4）用${ }包裹变量
5）利用数组返回多个值
6）参数存在默认值
7）let与const关键字：let与var差不多，只是被限定在特定范围使用；const定义常量；
8）for of值得遍历
    var someArray = [ "a", "b", "c" ];
    for (v of someArray) {
        console.log(v);//输出 a,b,c
    }
9）Promises：处理异步的模式，绑定了.when(), .done()等事件处理程序
```
16. 写代码
```
1. 继承实现
2. setTimeout相关
function a() {
    console.log('hello');
};
a();
setTimeout("console.log('over')", 3000);
```

[返回目录](../../CONTENTS.md)