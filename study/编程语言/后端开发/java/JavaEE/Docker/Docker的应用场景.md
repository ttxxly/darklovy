Docker 是一个开源的应用容器引擎，基于 [Go 语言](http://www.runoob.com/go/go-tutorial.html) 并遵从Apache2.0协议开源。

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

## Docker的应用场景

- Web 应用的自动化打包和发布。
- 自动化测试和持续集成、发布。
- 在服务型环境中部署和调整数据库或其他的后台应用。
- 从头编译或者扩展现有的OpenShift或Cloud Foundry平台来搭建自己的PaaS环境。

## Docker 的优点

- **1、简化程序：**
  Docker  让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux  机器上，便可以实现虚拟化。Docker改变了虚拟化的方式，使开发者可以直接将自己的成果放入Docker中进行管理。方便快捷已经是  Docker的最大优势，过去需要用数天乃至数周的	任务，在Docker容器的处理下，只需要数秒就能完成。
- **2、避免选择恐惧症：**
  如果你有选择恐惧症，还是资深患者。Docker  帮你	打包你的纠结！比如 Docker 镜像；Docker 镜像中包含了运行环境和配置，所以 Docker 可以简化部署多种应用实例工作。比如  Web 应用、后台应用、数据库应用、大数据应用比如 Hadoop 集群、消息队列等等都可以打包成一个镜像部署。
- **3、节省开支：**
  一方面，云计算时代到来，使开发者不必为了追求效果而配置高额的硬件，Docker 改变了高性能必然高价格的思维定势。Docker 与云的结合，让云空间得到更充分的利用。不仅解决了硬件管理的问题，也改变了虚拟化的方式。

### Docker 架构

Docker 使用客户端-服务器 (C/S) 架构模式，使用远程API来管理和创建Docker容器。Docker 容器通过 Docker 镜像来创建。容器与镜像的关系类似于面向对象编程中的对象与类。 [3]  

| Docker | 面向对象 |
| ------ | -------- |
| 容器   | 对象     |
| 镜像   | 类       |

 [ ![img](https://gss2.bdstatic.com/9fo3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D220/sign=b2a57334b2a1cd1101b675228913c8b0/a50f4bfbfbedab644936dac4ff36afc379311e69.jpg) ](https://baike.baidu.com/pic/Docker/13344470/0/a50f4bfbfbedab644936dac4ff36afc379311e69?fr=lemma&ct=single) 

Docker daemon 一般在宿主主机后台运行，等待接收来自客户端的消息。 Docker 客户端则为用户提供一系列可执行命令，用户用这些命令实现跟 Docker daemon 交互。

### 特性

在docker的网站上提到了docker的典型场景：

- Automating the packaging and deployment of applications（使应用的打包与部署自动化）
- Creation of lightweight, private PAAS environments（创建轻量、私密的PAAS环境）
- Automated testing and continuous integration/deployment（实现自动化测试和持续的集成/部署）
- Deploying and scaling web apps, databases and backend services（部署与扩展webapp、数据库和后台服务）

由于其基于LXC的轻量级虚拟化的特点，docker相比KVM之类最明显的特点就是启动快，资源占用小。因此对于构建隔离的标准化的运行环境，轻量级的PaaS(如dokku),  构建自动化测试和持续集成环境，以及一切可以横向扩展的应用(尤其是需要快速启停来应对峰谷的web应用)。

1. 构建标准化的运行环境，现有的方案大多是在一个baseOS上运行一套puppet/chef，或者一个image文件，其缺点是前者需要base  OS许多前提条件，后者几乎不可以修改(因为copy on write 的文件格式在运行时rootfs是read  only的)。并且后者文件体积大，环境管理和版本控制本身也是一个问题。
2. PaaS环境是不言而喻的，其设计之初和dotcloud的案例都是将其作为PaaS产品的环境基础
3. 因为其标准化构建方法(buildfile)和良好的REST API，自动化测试和持续集成/部署能够很好的集成进来
4. 因为LXC轻量级的特点，其启动快，而且docker能够只加载每个container变化的部分，这样资源占用小，能够在单机环境下与KVM之类的虚拟化方案相比能够更加快速和占用更少资源

### 局限

Docker并不是全能的，设计之初也不是KVM之类虚拟化手段的替代品，简单总结几点：

1. Docker是基于Linux 64bit的，无法在32bit的linux/Windows/unix环境下使用
2. LXC是基于cgroup等linux kernel功能的，因此container的guest系统只能是linux base的
3. 隔离性相比KVM之类的虚拟化方案还是有些欠缺，所有container公用一部分的运行库
4. 网络管理相对简单，主要是基于namespace隔离
5. cgroup的cpu和cpuset提供的cpu功能相比KVM的等虚拟化方案相比难以度量(所以dotcloud主要是按内存收费)
6. Docker对disk的管理比较有限
7. container随着用户进程的停止而销毁，container中的log等用户数据不便收集

针对1-2，有windows base应用的需求的基本可以pass了; 3-5主要是看用户的需求，到底是需要一个container还是一个VM, 同时也决定了docker作为 IaaS 不太可行。

针对6,7虽然是docker本身不支持的功能，但是可以通过其他手段解决(disk quota, mount --bind)。总之，选用container还是vm, 就是在隔离性和资源复用性上做权衡。

另外即便docker  0.7能够支持非AUFS的文件系统，但是由于其功能还不稳定，商业应用或许会存在问题，而AUFS的稳定版需要kernel 3.8,  所以如果想复制dotcloud的成功案例，可能需要考虑升级kernel或者换用ubuntu的server版本(后者提供deb更新)。这也是为什么开源界更倾向于支持ubuntu的原因(kernel版本)

 [ ![img](https://gss1.bdstatic.com/-vo3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D220/sign=4fb327646a224f4a5399741139f69044/9213b07eca806538f19ff55190dda144ad34827f.jpg) ](https://baike.baidu.com/pic/Docker/13344470/0/9213b07eca806538f19ff55190dda144ad34827f?fr=lemma&ct=single) 

Docker并非适合所有应用场景，Docker只能虚拟基于Linux的服务。Windows Azure 服务能够运行Docker实例，但到目前为止Windows服务还不能被虚拟化。

可能最大的障碍在于管理实例之间的交互。由于所有应用组件被拆分到不同的容器中，所有的服务器需要以一致的方式彼此通信。这意味着任何人如果选择复杂的基础设施，那么必须掌握应用编程接口管理以及集群工具，比如Swarm、Mesos或者Kubernets以确保机器按照预期运转并支持故障切换。

Docker在本质上是一个附加系统。使用文件系统的不同层构建一个应用是有可能的。每个组件被添加到之前已经创建的组件之上，可以比作为一个文件系统更明智。分层架构带来另一方面的效率提升，当你重建存在变化的Docker镜像时，不需要重建整个Docker镜像，只需要重建变化的部分。

可能更为重要的是，Docker旨在用于弹性计算。每个Docker实例的运营生命周期有限，实例数量根据需求增减。在一个管理适度的系统中，这些实例生而平等，不再需要时便各自消亡了。

针对Docker环境存在的不足，意味着在开始部署Docker前需要考虑如下几个问题。首先，Docker实例是无状态的。这意味着它们不应该承载任何交易数据，所有数据应该保存在数据库服务器中。

其次，开发Docker实例并不像创建一台虚拟机、添加应用然后克隆那样简单。为成功创建并使用Docker基础设施，管理员需要对系统管理的各个方面有一个全面的理解，包括Linux管理、编排及配置工具比如Puppet、Chef以及Salt。这些工具生来就基于命令行以及脚本。 

### 原理

Docker核心解决的问题是利用LXC来实现类似VM的功能，从而利用更加节省的硬件资源提供给用户更多的计算资源。同VM的方式不同, [LXC](https://baike.baidu.com/item/LXC) 其并不是一套硬件虚拟化方法 - 无法归属到全虚拟化、部分虚拟化和半虚拟化中的任意一个，而是一个操作系统级虚拟化方法, 理解起来可能并不像VM那样直观。所以我们从虚拟化到docker要解决的问题出发，看看他是怎么满足用户虚拟化需求的。

用户需要考虑虚拟化方法，尤其是硬件虚拟化方法，需要借助其解决的主要是以下4个问题:

- 隔离性 - 每个用户实例之间相互隔离, 互不影响。 硬件虚拟化方法给出的方法是VM, LXC给出的方法是container，更细一点是kernel namespace
- 可配额/可度量 - 每个用户实例可以按需提供其计算资源，所使用的资源可以被计量。硬件虚拟化方法因为虚拟了CPU, memory可以方便实现, LXC则主要是利用cgroups来控制资源
- 移动性 - 用户的实例可以很方便地复制、移动和重建。硬件虚拟化方法提供snapshot和image来实现，docker(主要)利用AUFS实现
- 安全性  -  这个话题比较大，这里强调是host主机的角度尽量保护container。硬件虚拟化的方法因为虚拟化的水平比较高，用户进程都是在KVM等虚拟机容器中翻译运行的,  然而对于LXC, 用户的进程是lxc-start进程的子进程, 只是在Kernel的namespace中隔离的,  因此需要一些kernel的patch来保证用户的运行环境不会受到来自host主机的恶意入侵, dotcloud(主要是)利用kernel  grsec patch解决的.

转载自：https://baike.baidu.com/item/Docker/13344470?fr=aladdin