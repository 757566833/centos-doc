docker-测18.09.5
1. 查看内核版本
```
uname -r
``` 
必须高于3.10
2. 删除没鸟用的
```
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```
3. 安装系统工具
```
yum install -y yum-utils device-mapper-persistent-data lvm2
```
4. 添加源
```
 yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```
5. 更新
```
 yum makecache fast
```
6. 安装
```
yum -y install docker-ce
vim /usr/lib/systemd/system/docker.service
14行注释掉
复制一行出来
/xxx 是存储的目标路径
ExecStart=/usr/bin/dockerd --graph /xxx -H fd:// --containerd=/run/containerd/containerd.sock

在我们公司的服务器 我将/xxx 设置为/file/gitlab
```
7. 启动
```
systemctl start docker
```
8. 看一下镜像
```
docker search centos
```
9. 拉镜像
```
docker pull centos
```
10. 新建容器
```
 docker run -t -i centos  /bin/bash
```
11. 查看容器id
```
docker ps -a
```
12. 启动容器
```
docker start <id>
```
13. 进入容器
```
docker exec -i -t <id> /bin/bash
```