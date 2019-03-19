# 运行应用
* 运行容器化应用
* Kubernetes通过各种Controller管理Pod的生命周期，为了满足不同的业务场景，Kubernetes开发了Deployment、ReplicaSet、DaemonSet、StatefuleSet、Job等多种Controller

## 运行Deployment
* 运行一个Deployment
```
kubectl run nginx-deployment --image=nginx:1.7.9 --replicas=2
```
即：部署包含两个副本的Deployment nginx-deployment，容器的image为nginx:1.7.9

[返回目录](../CONTENTS.md)