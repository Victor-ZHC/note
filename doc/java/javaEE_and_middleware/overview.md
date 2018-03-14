# Overview
## 组件
* 自包含的功能软件单元，包括：Web组件和EJB组件
* Web组件，如：servlet, JSP
* EJB组件，如：enterprise bean
    * 两种类型的enterprise bean: session bean和message-driven bean
    * Session Bean：为客户端提供服务，分为两种，有状态（每次返回新的SessionBean）和无状态（每次返回同一个SessionBean）
    * Message Driven Bean，基于JMS（Java Message Service），有两种工作模型：p2p（点对点），发布订阅模型

## 容器
* 支持组件和底层平台功能的接口，3类：
    1. Java EE服务器，包括：EJB容器和Web容器
    2. 应用客户端容器
    3. Applet容器

## 部署描述文件
* 2种：
    1. Java EE部署描述文件
    2. 运行时部署描述文件

## 四种类型的JavaEE模块
* EJB模块
* Web模块
* Application Client模块
* Resource Adapter模块

## JSTL
* JSP标准标签库（JavaServer Pages Standard Tag Library）

## JPA
* Java Persistence API
* 将运行对象持久化到数据库中
* 注：Java持久化包括三部分：
    1. JPA；
    2. 查询语句；
    3. 对象/关系 映射元数据；

## JTA
* Java Transaction API

## JAX-RS
* Java API for RESTful Web Services

## JMS
* Java Message Service API
* create, send, receive and read messages

## SSH框架
* Struts：表示层 
* Spring：应用层、业务层
* Hibernate：持久层、数据层

[返回目录](../CONTENTS.md)