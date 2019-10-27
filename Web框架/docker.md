#### docker在ubuntu镜像的安装

```
 curl -fsSL get.docker.com -o get-docker.sh
 sudo sh get-docker.sh --mirror Aliyun
```
#### 提升权限

```
sudo groupadd docker
sudo gpasswd -a ${USER} docker
sudo service docker restart
newgrp - docker
```
#### docker加速器

```
cd /etc/docker
vim daemon.json
 
添加内容
----
{
  "registry-mirrors": [
    "https://registry.docker-cn.com"
  ]
}
----
sudo systemctl daemon-reload
sudo systemctl restart docker
```
### 启动tomcat
```
docker run -p 8080:8080 tomcat
```
