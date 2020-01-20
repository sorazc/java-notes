# Docker

## 安装

### windows7

安装docker-toolbox

[下载地址](http://mirrors.aliyun.com/docker-toolbox/windows/docker-toolbox/)
#### 镜像加速
替换网易镜像 http://hub-mirror.c.163.com

执行以下四行代码
```
docker-machine ssh default
sudo sed -i "s|EXTRA_ARGS='|EXTRA_ARGS='--registry-mirror=http://hub-mirror.c.163.com |g" /var/lib/boot2docker/profile
exit
docker-machine restart default
```