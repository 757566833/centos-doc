1.安装docker
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