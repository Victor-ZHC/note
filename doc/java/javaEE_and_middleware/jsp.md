# JSP技术
## JSP
* Tomcat上最终执行Servlet类，以Servlet访问服务器
* 分为
    1. 动态内容，JSP元素：同Servlet；
    2. 静态内容；
* 优点：编译自动完成；
* 缺点：开发不知正确与否；

## JSP元素（动态内容）
### 包括：
1. 指令：控制如何翻译；
2. 脚本元素（Servlet方法）；
3. 表达式语法；
4. jsp:[set|get]Property；
5. jsp:[include|forward]；
6. jsp:plugin；
7. 定制标签；

## JSP标准语法
* 注释 <%--  —%>
* 声明 <%!  %> 
* 指令 <%@  %>
    * 包含include，页面page，标签库taglib
* 表达式 <%=  %>
* 脚本 <%  %>

## 指令
* @page 控制不同的执行参数，名值对，中间以逗号隔开
    * session：servlet缺省无session，而JSP默认session=“true”
    * import：导入包，以逗号隔开，常用包已默认导入
    * extends：扩展其他类
    * contentType：“text/html, charset=GBK”，设置文本类型和字符编码
    * buffer：输出先到缓冲区，缺省8192KB，JSP缺省有缓冲区，而servlet缺省无缓冲区，通过response.setBuffer(8192); 设置缓冲区
    * ThreadSafe：一般isThreadSafe=“true”，允许多线程
    * errorPage：页面异常，isErrorPage=”true”，表示是错误页面
* @include
    * 属性file，静态过程，类似于宏替换，优点：重用
    * servlet是通过请求分派器请求分派
* @taglib 定制标签
    * TLD：.tld文件，是XML文件格式
    * 标签处理器类：有 doTag() 和 set() 方法

## 脚本
* 创建实例变量或类变量，要在声明中创建

## 表达式
* 计算表达式，转换成String对象，插入到输出流中