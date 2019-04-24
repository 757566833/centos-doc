svnserve 1.7.14
1. 安装
```
yum install subversion
```
2. 检查安装成功
```
svnserve --version
```
3. 建立版本库
```
mkdir /xxx          //  公司的/file/svn
cd /xxx
svnadmin create /xxx/svnrepos 
```
4. 账号密码设置
```
cd /xxx/svnrepos/conf/
vi passwd

// user标签下 追加
<账号> = <密码>
// 保存退出

vi authz
文件末尾添加
[/]
<账号>=<权限>

// 例如 zhangsan=rw
```
5. 服务配置
```
vi svnserve.conf

anon-access = read    // 匿名用户可读，您也可以设置 anon-access = none，不允许匿名用户访问。设置为 none，可以使日志日期正常显示
auth-access = write   // 授权用户可写
password-db = passwd  // 使用哪个文件作为账号文件
authz-db = authz      // 使用哪个文件作为权限文件
realm = /xxx/svnrepos // 认证空间名，版本库所在目录
```
6. 启动
```
svnserve -d -r /xxx
```
7. 开机启动
```
vim /etc/rc.d/rc.local
/usr/bin/svnserve -d -r /file/svn/
```
本服务器 放在 /file/svn 下