3.0.2
```
yum install -y vsftpd 
```
```
service vsftpd start
```
```
// 开机启动
systemctl enable vsftpd
```
```
关闭匿名访问

/etc/vsftpd/vsftpd.conf
// 12行 
anonymous_enable=NO
// 101行
chroot_local_user=YES

// 添加一行
local_root=/xxx  所有用户都进这个目录，主要是因为根目录不能直接用比较尴尬
```
------
### 遇到的坑
根目录 不可以777权限 所以 根目录下新建个文件夹 才可以继续
或者 根目录下所有文件 777