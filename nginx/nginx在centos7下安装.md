# Nginx安装

## 1 前言
centOS 7 默认仓库没有nginx, 通过yum源进行安装Nginx

[文档](http://nginx.org/en/linux_packages.html)

## 2 安装

#### 2.1 下载Nginx的repo源
```
wget http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
```
#### 2.2 将Nginx添加到系统的yum库
在使用nginx存储库时，默认情况下会选择nginx的最新稳定版本进行安装
```
rpm -ivh nginx-release-centos-7-0.el7.ngx.noarch.rpm
```
#### 2.4 安装nginx
```
yum -y install nginx
```
## 3 运行
#### 3.1 启动nginx服务
```
systemctl start nginx
```
#### 3.2 检查其运行状态
```
systemctl status nginx
```
#### 3.3 开机启动Nginx服务
```
systemctl enable nginx
```
#### 3.4 防火墙
如果正在运行防火墙，则还需要打开HTTP和HTTPS端口80和443：
```
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
```
### 4 常用命令
停止Nginx服务：
```
systemctl stop nginx
```
再次启动：
```
systemctl start nginx
```
重新启动：
```
systemctl restart nginx
```
在进行一些配置更改后重新加载Nginx
```
systemctl reload nginx
```
禁用Nginx开机启动
```
systemctl disable nginx
```
开启Nginx开机启动
```
systemctl enable nginx
```
### 5 配置
nginx配置文件位于：/etc/nginx/nginx.conf