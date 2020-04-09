
+++
title = "filebrowser 安装及使用"
date= '2020-04-06'
draft= false
tags = ['filebrowser','服务器文件管理','linux','简易网盘']
categories = ['兴趣']
+++



## 简介  
File Browser 是一个基于 Web 的文件管理器。它可以使你随时随地的对设备的文件进行基本的管理操作，如：创建、删除、移动、复制等。它支持多个用户的管理，而且每个用户可以拥有自己可以访问的文件和权限。它还支持文件分享。你还可以用它来执行一些 Linux 命令，比如你想要在当前目录下克隆一个代码库，就可以用它来执行git等命令。
<!--more-->  

## 安装及配置
- File Browser 为单文件，下载后即可用。

- 创建配置数据库： 
```
filebrowser -d /etc/filebrowser.db config init
```
- 设置监听地址：  
```
filebrowser -d /etc/filebrowser.db config set --address 0.0.0.0  
```
- 设置监听端口：  
```
filebrowser -d /etc/filebrowser.db config set --port 8088  
```
- 设置语言环境：  
```
filebrowser -d /etc/filebrowser.db config set --locale zh-cn  
```
- 设置日志位置：  
```
filebrowser -d /etc/filebrowser.db config set --log /var/log/filebrowser.log  
```
- 添加一个用户：  
```
filebrowser -d /etc/filebrowser.db users add root password --perm.admin  
```
 其中的root和password分别是用户名和密码，根据自己的需求更改。
```
文件根目录：
```
filebrowser -d /etc/filebrowser.db config set --root /path/to/root  
```
```  

- 更多配置： https://docs.filebrowser.xyz/  

- 配置修改好以后，就可以启动 File Browser 了，使用-d参数指定配置数据库路径。  
```
filebrowser -d /etc/filebrowser.db  
```

## 后台运行  

- 第一种是 nohup 大法：  
```
 nohup filebrowser -d /etc/filebrowser.db >/dev/null 2>&1 &  
```

停止运行：`kill -9 $(pidof filebrowser)`   

开机启动：  
```
sed -i '/exit 0/i\nohup filebrowser -d \/etc\/filebrowser.db >\/dev\/null 2>&1 &' /etc/rc.local
```

取消开机启动：  
```
sed -i '/nohup filebrowser -d \/etc\/filebrowser.db >\/dev\/null 2>&1 &/d' /etc/rc.local  
```

- 第二种是 systemd 大法：

1. 编写service文件  
```
vim /etc/systemd/system/filebrowser.service  
```
ExecStart根据自己的实际目录修改  
```
[Unit]
Description=File Browser
After=network.target

[Service]
ExecStart=/filebrowser/filebrowser -d /filebrowser/filebrowser.db

[Install]
WantedBy=multi-user.target  
```
2. 启动及开机自启  
```
systemctl daemon-reload  
systemctl start filebrowser  
systemctl enable filebrowser  
```


