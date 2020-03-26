# centos7系统的基础优化脚本

涉及内容： 1.DNS 2.网络yum源 3.epel源 4.同步时间 5.安装vim 6.设置最大打开文件描述符数 7.禁用selinux 8.关闭防火墙 9.优化ssh连接速度 10.内核参数优化 11.设置vim退格键删除最后一个字符类型 12.更新内核 

```text
#!/bin/bash
#author yundd by 
#this script is only for CentOS 7.x
#check the OS

platform=`uname -i`
if [ $platform != "x86_64" ];then 
echo "this script is only for 64bit Operating System !"
exit 1
fi
echo "the platform is ok"
cat << EOF
 your system is CentOS 7 x86_64  
EOF

#添加公网DNS地址
cat >> /etc/resolv.conf << EOF
nameserver 114.114.114.114
EOF
#Yum源更换为国内阿里源
yum install wget -y
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

#添加阿里的epel源
#add the epel
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
# rpm -ivh http://dl.Fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-8.noarch.rpm

#yum重新建立缓存
yum clean all
yum makecache
#同步时间
 ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
yum -y install ntp
/usr/sbin/ntpdate cn.pool.ntp.org
echo "* 4 * * * /usr/sbin/ntpdate cn.pool.ntp.org > /dev/null 2>&1" >> /var/spool/cron/root
systemctl  restart crond.service

#安装vim
yum -y install vim
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
#安装lrzsz实现win与linux之间的文件互相下载上传
yum -y install lrzsz

#设置最大打开文件描述符数
echo "ulimit -SHn 102400" >> /etc/rc.local
cat >> /etc/security/limits.conf << EOF
*           soft   nofile       655350
*           hard   nofile       655350
EOF


#禁用selinux
sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
setenforce 0

#关闭防火墙
systemctl disable firewalld.service 
systemctl stop firewalld.service 

#set ssh
sed -i 's/^GSSAPIAuthentication yes$/GSSAPIAuthentication no/' /etc/ssh/sshd_config
sed -i 's/#UseDNS yes/UseDNS no/' /etc/ssh/sshd_config
systemctl  restart sshd.service


#内核参数优化
#更新中

#vim定义退格键可删除最后一个字符类型
echo 'alias vi=vim' >> /etc/profile
echo 'stty erase ^H' >> /etc/profile
cat >> /root/.vimrc << EOF
set tabstop=4
set shiftwidth=4
set expandtab
syntax on
"set number
EOF

# update soft
yum -y update
```



