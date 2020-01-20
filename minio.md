# minIO

## 1 文档

[github](https://github.com/minio/minio/blob/master/README_zh_CN.md)

[官网](https://docs.min.io/cn/)

## 2 安装
docker
```
docker pull minio/minio
```
## 3 docker运行
### 3.1 指定储存路径
MinIO 需要一个持久卷来存储配置和应用数据。不过, 如果只是为了测试一下, 您可以通过简单地传递一个目录（在下面的示例中为/ data）启动MinIO。这个目录会在容器启动时在容器的文件系统中创建，不过所有的数据都会在容器退出时丢失。
```
docker run -p 9000:9000 minio/minio server /data
```
要创建具有永久存储的MinIO容器，您需要将本地持久目录从主机操作系统映射到虚拟配置~/.minio 并导出/data目录。 为此，请运行以下命令

GNU/Linux 和 macOS

```
docker run -p 9000:9000 --name minio1 \
  -v /mnt/data:/data \
  -v /mnt/config:/root/.minio \
  minio/minio server /data
```
Windows
```
docker run -p 9000:9000 --name minio1 \
  -v D:\data:/data \
  -v D:\minio\config:/root/.minio \
  minio/minio server /data
```
### 3.2 自定义Access和Secret密钥
GNU/Linux 和 macOS
```
docker run -p 9000:9000 --name minio1 \
  -e "MINIO_ACCESS_KEY=AKIAIOSFODNN7EXAMPLE" \
  -e "MINIO_SECRET_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY" \
  -v /mnt/data:/data \
  -v /mnt/config:/root/.minio \
  minio/minio server /data
```
Windows
```
docker run -p 9000:9000 --name minio1 \
  -e "MINIO_ACCESS_KEY=AKIAIOSFODNN7EXAMPLE" \
  -e "MINIO_SECRET_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY" \
  -v D:\data:/data \
  -v D:\minio\config:/root/.minio \
  minio/minio server /data
```