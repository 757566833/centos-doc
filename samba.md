# samba 4.8.3-4.e17
```
yum install samba -y
```
```
vim /etc/samba/smb.config
// global 中加入
map to guest = Bad User  // 开启匿名访问

```
在下面添加share标签
```
[share]
    comment = share
    path = /xxx              // 想分享的目录
    browseable = yes
    read only = yes          // 防止手误
    guest ok = yes
```
## 遇到的问题
windows 关闭安全策略

win+r  输入gpedit.msc  计算机配置=》 管理模板 =》 网络 =》 lanman工作站

在右侧选第三个 启用不安全的来宾登陆 

双击 =》选启动=》应用