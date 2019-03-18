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
* 是计算、存储和网络资源的集合

### Master
* 是Cluster的大脑，主要职责是调度，即决定将应用放在哪里运行
* 为实现高可用，可以运行多个Master

### Node
* 职责是运行容器应用
* 由Master管理，负责监控并汇报容器状态
* 根据Master的要求管理容器的生命周期

### Pod
* 是Kubernetes的最小工作单元
* 每个Pod包含一个或多个容器
* Pod中的容器会作为整体被Master调度到一个Node上运行
* Pod中的所有容器使用同一个网络namespace，即相同的IP地址和Port空间，相互可以直接用localhost通信

### Controller
* Kubernetes通常不会直接创建Pod，而是通过Controller来管理Pod，Controller中定义了Pod的部署特性，Kubernetes提供了多种Controller，包括：Deployment、ReplicaSet、DaemonSet、StatefuleSet、Job等

### Service
* Kubernetes Service定义了外界访问一组特定Pod的方式，Service有自己的IP和端口，Service为Pod提供了负载均衡
* Kubernetes运行容器（Pod）与访问容器（Pod）两项任务分别由：Controller和Service执行

### Namespace
* Namespace将物理的Cluster逻辑上划分为多个虚拟Cluster，每个Cluster是一个Namespace，不同Namespace的资源完全隔离
* Kubernetes默认创建了两个Namespace，default和kube-system

## 部署Kubernetes Cluster
### 安装Docker
* 所有节点都需要安装Docker
* 安装命令：
```
> apt-get update && apt-get install docker.io
```

### 安装kubelet、kubeadm和kubectl
* kubelet：运行在cluster所有节点上，负责启动Pob和容器
* kubeadm：用于初始化Cluster
* kubectl：Kubernetes命令行工具，可以部署和管理应用，查看各种资源，创建、删除和更新各种组件

[返回目录](../CONTENTS.md)