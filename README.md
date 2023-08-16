# Mymonitor
分布式Linux性能监控
# 环境配置
ubuntu 20.04  net模式 硬盘大小30-40G
# docker安装
安装 curl下载docker脚本 命名为test-docker.sh：

curl -fsSL https://test.docker.com -o test-docker.sh

执行脚本，自动帮我们安装docker：

sudo sh test-docker.sh
# 项目简介
1、docker模块：dockerfile指定相应的cmake，grpc，proto等源码和依赖，构建整个项目环境，易于在多台服务器上部署环境，并编写容器操作的脚本指令，易于启动操作项目所依赖的环境。

2、monitor模块：采用工厂方法，通过构造moniotr的抽象类定义接口，后实现相应的CPU状态，系统负载，软中断，mem，net监控，易于为之后扩展更多系统监控；并为了模拟出真实的性能问题，使用stress工具进行模拟压测，分析相应时刻服务器的cpu状况和中断状况。

3、通过grpc框架，构建出相应的server，client；server在所要监控的服务器部署，client生成库供monitor模块和display模块调用，并考虑为了降低耦合性，项目每个模块相互独立，可拆解，只通过调用grpc服务来进行远程连接。

4、使用protobuf序列化协议，构建出整个项目的数据结构。

5、display模块分为两大部分：ui界面的构造，datamodel构造；

ui界面使用QWidget、QTableView、QStackedLayout、QPushButton等进行构建

datamodel：通过继承QAbstractTableModel，构建出相应的cpu_model、softirq_model、mem_model等，每3秒刷新一次数据。

# 博客地址
https://blog.csdn.net/super8ayan/category_12376431.html?spm=1001.2014.3001.5482

# 项目演示
**路径：/docker/scriptsmm**

启动容器：
./monitor_docker_run.sh

进入容器：
./monitor_docker_into.sh

## 本地监控

**路径：/work/cmake/test_monitor/src**

启动RPC模块：./server

**路径：/work/cmake/test_monitor/src**

启动monitor模块：./monitor

**路径：/work/cmake/display_monitor**

启动显示qt：./display

![image](https://github.com/8upersaiyan/Mymonitor/blob/main/1.png)


## 远程监控

客户端中的rpc_manager中的rpc_client构造函数中gRPC连接通道IP需要修改成我们需要监听的目标服务器IP地址
  
    auto channel = grpc::CreateChannel("localhost:50051", grpc::InsecureChannelCredentials());
    =》 auto channel = grpc::CreateChannel("192.168.11.129:50051", grpc::InsecureChannelCredentials());

只需在服务端启动gRPC模块和monitor监控模块，客户端启动gRPC模块和display模块即可展示出服务器的信息

可实现在一台客户端监控多台服务器的信息，只需更改gRPC连接IP即可。

## 使用stress压测指令

模拟系统负载较高时的场景

    消耗CPU资源：$ stress -c 2 使用两个进程不断计算随机数的平方根
    消耗内存资源：$ stress --vm 2 --vm-bytes 300M --vm-keep  产生两个子进程，每个进程分配 300M 内存
    消耗IO资源：$ stress -i 2 每个进程都反复调用 sync 函数将内存上的内容写到硬盘上
    消耗磁盘及IO：$ stress -d 1 --hdd-bytes 10M 创建一个进程不断的在磁盘上创建 10M 大小的文件并写入内容








