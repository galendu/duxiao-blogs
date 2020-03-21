# Failed to get D-Bus connection: Operation not permitted

docker中安装完httpd服务后，使用命令`systemctl start httpd.service`，发现报错，错误信息：`Failed to get D-Bus connection: Operation not permitted`

解决方法：使用命令`docker run -d -name centos7 --privileged=true centos:7 /usr/sbin/init`创建容器，然后使用`docker exec -it centos7 /bin/bash`进入容器

