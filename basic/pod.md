# kubernetes的基本概念

### 什么是容器？

容器就是视图隔离、资源可以限制、独立文件系统的进程集合。在以往的服务中，很多进程都存在一些特点：进程之间可以相互通信，并且是可见的；进程与进程之间可以在相同的文件上进行读写；进程可能会占用过多的资源，导致其他进程低效。这些问题的解决办法是：使用namespace技术在资源上试图进行隔离；使用chroot技术来解决文件之间的问题；使用Cgroup来解决进程资源的问题。在这样的一个催生下，便可以使用这些特征来定义这些进程集合，那便是容器。

### 什么是镜像？

容器运行所需要的所有文件的集合称之为镜像。

### 容器与VM

VM利用Hypervisor虚拟化技术来模拟CPU、内存等硬件资源，这样就可以在宿主机上面建立一个Guest OS，每一个OS都有一个独立的内核，这样应用之间是相互独立的，那么很好的提供了一个隔离，但是这样的缺点便是将资源交给虚拟化，无法充分利用计算资源，并且占据着巨大的磁盘资源。这个时候即便催生了容器。

容器是针对进程而言的，无需Guest OS,只需要独立的文件系统，所有的文件隔离都是进程级别，那么相比于VM要更快一些，但是进程级别的隔离并没有VM那么好。

### 什么是Kubernetes Master?

kubernetes里的Master指的是集群控制节点，每一个kubernetes集群需要有一个Master节点来负责整个集群的管理和控制，基本上kubernetes的所有控制命令都是在Master节点上运行。

### 什么是Kubernetes Node?

Node节点是kubernetes集群中的工作负载节点。可以是一台物理主机，也可以是一台虚拟机。

### 什么是Pod?

是kubernetes的最小调度资源以及资源单元。它是由一个或者多个容器组成。

### 什么是Replication Controller？

RC是kubernetes系统中的核心概念之一，它定义了一个期望的场景，即声明某种Pod的副本数量在任意时刻都符合某一个预期值。**（与Kubernetes代码中模块Replication Controller同名，所以升级成了一个Replica Set）**

### 什么是Replica Set？

与Replication Controller不同的是，Replica Set支持基于集合的Label Selector,而与RC只支持基于等式的Label Selector。

### 什么是Volume?

Volume就是卷的概念，是用来管理kubernetes的存储的，它可以挂载在一个或者多个容器的指定路径下，支持多种后端存储的抽象，比如像ceph,GlusterFS。

### 什么是Horizontal Pod Autoscaler？

通过追踪分析RC控制所有的目标Pod的负载变化情况，来确定那些需要针对性的调整资源；这就是HPA。

### 什么是Deployment?

Deployment是Pod的更上一层的抽象，它可以定义Pod的副本数，以及这个Pod的版本等信息。一般都是使用Deployment来做应用真正的管理。

### 什么是Service?

Service提供一个或者多个Pod实例稳定的访问地址。支持多种访问方式：ClusterIP、NodePort、LoadBalancer。

### 什么是Namespace?

namespaces是用来做内部的逻辑隔离的，包括了权限、资源等。

### 什么是annotation?

用key-value的方式进行定义，但是它可以添加用户自定义的附加信息，比如build信息，release信息等。

### 什么是Label?

Label是kubernetes系统中的一个核心概念。一个Label是一个key-value的键值对，其中key与value由用户自己指定。Label可以附加到各种资源对象上，例如：Node、Pod、Service、RC等，一个资源对象可以定义任意数量的Label。



