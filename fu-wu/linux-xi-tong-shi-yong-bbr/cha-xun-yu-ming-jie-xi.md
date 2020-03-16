# 查询域名解析

## 1.第一种方法

查询域名解析命令一般用dig查询，这个命令需要在linux下运行

dig命令安装

```bash
yum -y install bind-utils
```

运行查询

```bash
dig docs.os4.top +trace
```

### 2.第二种方式

{% embed url="http://www.kloth.net/services/dig.php" %}

Domain填写域名，并勾选trace，点击Look it up

