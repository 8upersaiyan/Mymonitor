# Mymonitor
分布式Linux性能监控
# 环境配置
ubuntu 20.04  net模式 硬盘大小30-40G
# docker安装
安装 curl下载docker脚本 命名为test-docker.sh：

curl -fsSL https://test.docker.com -o test-docker.sh

执行脚本，自动帮我们安装docker：

sudo sh test-docker.sh
# 项目演示
**路径：/docker/scriptsmm**

启动容器：
./monitor_docker_run.sh

进入容器：
./monitor_docker_into.sh

**路径：/work/cmake/test_monitor/src**

启动RPC模块：./server

**路径：/work/cmake/test_monitor/src**

启动monitor模块：./monitor

**路径：/work/cmake/display_monitor**

启动显示qt：./display

![image](https://github.com/8upersaiyan/Mymonitor/blob/main/1.png)








