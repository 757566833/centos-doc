# 系统版本  
## 安装过程
> 本文档仅限于支持uefi的主板 

1. 系统版本   
centos7 1810

2. u盘制作
UltraISO 直接制作uefi镜像u盘
（做windows系统直接将u盘改为gpt分区，镜像解压到根目录，插上就能用，centos未测试）    

3. bios设置
开机启动bios 改变开机启动项 如果没有uefi 就打开 然后u盘重插一次（部分主板子 改完biso需要重新注册硬件）

## 装机以后的问题
1. 第一个问题 
```
waring /dev/root does not exist

原因
//  一般来说是 centos做系统的时候 u盘名字不对 太长了 用UltraISO 就会出现这个问题
解决方式
// 随便改个名 这里我改成 CENTOS（随便改）

// 启动电脑后 在install的一个选项上按 e  （小写） 将路径（x20是空格的转译） 将路径改为 CENTOS（与上面对应）

// CTRL+X 接下来的安装就没啥问题了
```  



2. 第二个问题 开机后没网  

vi /etc/sysconfig/network-script/ifcfg-enp0s3 (这个文件名是当前系统的，不同版本不同名字)  

添加以下几行
```
DNS1=114.114.114.114
DNS2=8.8.8.8
GATEWAY=192.168.X.X     //简单来说就是你的路由器ip
IPADDR=X.X.X.X          //想设置的静态ip
NETMASK = 255.255.255.0 //子网掩码
```
修改两个参数
```
BOOTPROTO=static    // 原本是dhcp
ONBOOT=yes
```
存储
service network restart




3. 第三个问题  ssh 连不上
```
// 关闭防火墙
service firewalld stop
// 设置开机关闭
systemctl disable firewalld.service
```
```
// 关闭 selinux
setenforce 0
// 开机关闭
vim /etc/selinux/config  // selinux的值 设置为disable
```

## 硬盘相关

1. 挂载硬盘
新硬盘要进行分区  
```
fdisk -l  //查看所有硬盘
```
假设我的硬盘是sda

```
fdisk /dev/sda
```

p 显示磁盘分区 新硬盘是没东西的

n 新建分区

一路回车（只建立一个分区）

分完了 用p查看

w保存

2. 格式化硬盘 
```
mkfs.ext4 /dev/sda1  // 格式化
```
```
mount /dev/sda1 /xxx   // xxx是挂载路径
```
最后加一个开机自动挂载
```
// 用 命令  获取磁盘的uuid和属性
blkid

// 开机挂载配置
vim /etc/fstab

// 追加一段配置

// 配置模板：UUID=*************  /xxx  xxx（本教程是ext4）  defaults  1  1

// 这里有个隐藏的问题   顺序要按照 主板硬盘sata顺序 输入 后面1 1 第二个改成2 2 以此类推    不过也可能是我之前输错了
```