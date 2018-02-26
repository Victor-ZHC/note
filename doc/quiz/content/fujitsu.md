# 富士通
1. 线程唤醒
* notify()唤醒一个
* notifyAll()唤醒所有
2. 线程wait和sleep的区别
* Thread类的方法：sleep()，可以在任何地方使用
* Object类的方法：wait()和notify()，只能在同步控制块中使用
3. Session
* 创建：
    * 指令`<%@page session="true">`（注：Servlet缺省无Session，而JSP默认session="true"），若JSP中不写，则JSP文件被编译成Servlet时会有：
    `HttpSession session = HttpServletRequest.getSession(true);`
* 删除：
    * 调用HttpSession.invalidate()时
* 基本操作：
    * session.setAttribute(String key, Object obj);
    * session.getAttribute(String key);
4. 监听器
* 一般implements HttpSessionListener, ServletContextListener, ServletContextAttributeListener
* 贯穿整个Servlet生命周期，在web.xml中配置，类上有@WebListener
5. 过滤器
* implements Filter，有doFilter()方法，在web.xml中配置,类上有@WebFilter
6. Linux下的编辑器
   vi，gedit，emacs
7. Linux下上下左右移动
   上k 下j 左h 右l
8. Linux下复制一行yy  删除当前字符x

[返回目录](../CONTENTS.md)