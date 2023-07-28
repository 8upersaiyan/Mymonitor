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
/docker/scriptsmm目录下
启动容器：
./monitor_docker_run.sh


进入容器：
./monitor_docker_into.sh




