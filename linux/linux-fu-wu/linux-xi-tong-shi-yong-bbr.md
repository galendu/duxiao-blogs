---
description: 部署最新版内核，开启TCP BBR 加速
---

# linux系统使用bbr

{% hint style="success" %}
BBR是Google开发的一种新的拥塞控制算法
{% endhint %}

#### 1.安装elrepo的源,并下载内核

```bash
rpm --import  https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
yum install https://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm
```

#### 2.替换系统内核为支持bbr服务的内核，并设置启用bbr

```bash
yum --enablerepo=elrepo-kernel install kernel-ml -y 
egrep ^men /etc/grub2.cfg|cut -f 2 -d \'
# 设置默认内核启动项
grub2-set-default 0
reboot
# 启用bbr
echo 'net.core.default_qdisc=fq' | tee -a /etc/sysctl.conf
echo 'net.ipv4.tcp_congestion_control=bbr' | tee -a /etc/sysctl.conf
reboot
```

#### 3.生成一个10M的测试文件

```bash
dd if=/dev/zero of=./site.css count=1 bs=10M
```

4.测试下载速度

```bash
curl -o /dev/null http://os4.top/site.css
```

#### 5.elrepo地址

[地址](http://elrepo.org/tiki/tiki-index.php)

