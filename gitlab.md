1. 安装docker
2. 安装docker-compose
```
curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```
3. 权限
```
chmod +x /usr/local/bin/docker-compose
```
4. 查看安装状态
```
docker-compose --version
```
5. 打开别人的网站
https://github.com/sameersbn/docker-gitlab
6. 在一个空白文件夹下 下载(第五部的文档中提到)
```
wget https://raw.githubusercontent.com/sameersbn/docker-gitlab/master/docker-compose.yml
```
7. 安装
```
docker-compose up -d
```
8. 改配置（因为我们要放在别的硬盘）
```
//  实际上我们只改volumes
vim docker-compose.yml
//  改这条
volumes:
    - /file/gitlab/redis:/var/lib/redis:Z

//后面还有几个 都改掉 冒号前面是宿主机存储位置 后面是 docker存储位置 后面不变 在公司服务器 我将gitlab数据放入了 /file/gitlab下面
```
9. 重启
```
docker-compose down 
docker-compose up -d
```
访问ip：10080 得到服务

至此文件服务器完成了  
docker 放入/file/dockers 参照docker文档
gitlab放入 /file/gitlab

