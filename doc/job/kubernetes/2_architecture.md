# 架构设计
* Kubernetes Cluster由Master和Node组成，节点上运行着若干Kubernetes服务

## Master节点
* Master是Kubernetes Cluster的大脑，运行着的Daemon服务包括：kube-apiserver、kube-scheduler、kube-controller-manager、etcd和Pod网络
```
kube-apiserver：API Server提供HTTP/HTTPS RESTFUL API，是Kubernetes Cluster的前端接口
kube-scheduler：负责决定将Pod放在哪个Node上运行
kube-controller-manager：负责管理Cluster各种资源，保证资源处于预期的状态
etcd：负责保存Kubernetes Cluster的配置信息和各种资源的状态信息
Pod网络：Pod要能够相互通信，Kubernetes Cluster必须部署Pod网络
```

## Node节点
* Node是Pod运行的地方，Kubernetes支持Docker、rkt等容器Runtime。

[返回目录](../CONTENTS.md)