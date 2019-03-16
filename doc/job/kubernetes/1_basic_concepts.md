# 基础概念
* Kubernetes是Google Omega的开源版本，是目前发展最快、市场占有率最高的容器编排引擎产品，其功能包括：优化资源利用、高可用、滚动更新、网络插件、服务发现、监控、数据管理、日志管理等

## 基础命令
* 创建一个单节点的Kubernetes集群
```
> minikube start
> kubectl get nodes
```
* 查看集群信息
```
> kubectl cluster-info
```
* 部署应用
```
> kubectl run kubernetes-bootcamp \
    --image=docker.io/jocatalin/kubernetes-bootcamp:v1 \
    --port=8080
通过kubectl部署应用kubernetes-bootcamp，Docker镜像通过--image指定，--port设置应用对外服务的端口
```

## K8s重要术语-Pod
* Pod是容器的集合，通常会将紧密相关的一组容器放到一个Pod中，同一个Pod中的所有容器共享IP地址和Port空间，即：在一个network namespace中
* Pod是Kubernetes调度的最小单位，同一Pod中的容器始终被一起调度
* 查看当前Pod
```
> kubectl get pods
```

## 访问应用
* 默认情况下，所有Pod只能在集群内部访问；为了能够从外部访问应用，需要将容器的8080端口映射到节点的端口，执行命令：
```
> kubectl expose deployment/kubernetes-bootcamp \
    --type="NodePort" \
    --port 8080
```
* 查看应用被映射到节点的哪个端口
```
> kubectl get services
```

## Scale应用
* 默认情况下应用只运行一个副本，查看副本数命令：
```
> kubectl get deployments
```

## 滚动更新
* 当前使用的image版本为v1，执行如下命令后将其升级到v2：
```
> kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
```

## 重要概念
### Cluster
* 计算、存储和网络资源的集合

### Master
* Cluster的大脑

[返回目录](../CONTENTS.md)