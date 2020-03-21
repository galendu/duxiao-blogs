# start golang

## 简介

![golang](../.gitbook/assets/image%20%281%29.png)

## 安装golang

#### 1.windows系统安装golang

[https://golang.org/dl/](https://golang.org/dl/) 选择Microsoft Windows进行下载安装

#### 2.mac、linux系统安装golang

[https://golang.org/dl/](https://golang.org/dl/)  选择Linux版本的安装包

* 解压到/usr/local目录下

```text
tar -C /usr/local -xzf go*.linux-amd64.tar.gz 
```

* 创建环境变量，在/etc/profile文件或者$HOME/profile添加下面的内容，并使之生效

```text
export PATH=$PATH:/usr/local/go/bin
```

* 使用 `source /etc/profile` 使之生效

