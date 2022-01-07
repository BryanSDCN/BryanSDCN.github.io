[返回主页](index.md)

# Ubuntu搭建Ftp服务器

## 1. 安装vsftpd软件

命令： `sudo apt-get install vsftpd`

安装成功之后，默认的会在 文件系统下的srv 目录下创建一个ftp文件（和home在同一级目录下的），这里就是ftp服务器的默认文件夹！

在test文件夹中创建一个文件：`touch /srv/ftp/1.txt` 文件

重启一下！

命令是：`sudo /etc/init.d/vsftpd restart`

查看是否成功 找到Ubuntu的IP地址，在地址栏中访问  我的是：[ftp://127.0.0.1/]

ok！到此完成！

## 2. 修改配置

- 新建"/home/uftp"目录作为用户主目录  （用户 uftp）

```shell
sudo mkdir /home/uftp
sudo ls /home    (查看目录有没有生成)
```

- 新建用户uftp并设置密码

```shell
sudo useradd -d /home/uftp -s /bin/bash uftp (回车-->用户新建成功)
sudo passwd uftp (设置uftp用户的密码-->回车-->输入两次密码-->回车-->密码设置成功)
sudo chown uftp /home/uftp/ （修改文件夹的拥有者为uftp用户）
```

- 使用vi修改配置文件/etc/vsftpd.conf

`sudo vim /etc/vsftpd.conf`
 添加如下配置 ：

```shell
 userlist_deny=NO
 userlist_enable=YES
 userlist_file=/etc/allowed_users
 seccomp_sandbox=NO
 local_enable=YES
 pasv_promiscuous=YES
 write_enable=YES  （是否可写入）
```

 然后保存

- 使用vim新建/etc/allowed_users文件

```shell
sudo vim /etc/allowed_users 
```

(回车-->输入uftp-->保存， 文件创建成功)

- 查看 /etc/ftpusers文件中的内容
  看一看有没有uftp这个用户名，如果没有，就直接退出。如果有就删除uftp,因为这个文件中记录的是不能访问FTP服务器的用户清单
- 重启服务
  记着 `sudo service vsftpd restart`
- 直接浏览器访问 ftp：//主机ip地址，登录FTP服务器（ip可用ifconfig命令查看）
  按照提示输入 前面设置的用户名密码
  
[返回主页](index.md)

