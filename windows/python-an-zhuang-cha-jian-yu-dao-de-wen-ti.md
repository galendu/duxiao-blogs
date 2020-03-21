# python安装插件遇到的问题

### 1.安装pip install mysqlclient 解决mysql\_config:command not found

查看mysql\_config文件是否存在 find / -name mysql\_config

如果不存在，解决办法

```text
cd /etc/yum.repos.d/ 
wget http://repo.mysql.com/mysql57-community-release-el7-8.noarch.rpm
yum install mysql-devel
随后可进行 pip install mysqlclient 安装
```

### 2.更新中



