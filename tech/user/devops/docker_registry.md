
### Docker Registry

> 官网：
> - [docs.docker.com/registry](https://docs.docker.com/registry)


#### 安装使用

##### 服务端启动服务

```bash
# 1 拉取registry镜像
docker pull registry:2

# 2 创建docker容器
docker run  -d \
            -v /srv/run/dockerreg:/var/lib/registry \
            -p 5000:5000 \
            --name=registry-demo \
            --restart=always \
            registry:2
```

##### 客户端使用

```bash
# 1 docker镜像打标签，fisheep.cc为registry服务器的域名
docker tag ubuntu:20.04 fisheep.cc:5000/ubuntu:20.04

# 2 推送docker镜像
docker push fisheep.cc:5000/ubuntu:20.04

# 3 拉取docker镜像
docker pull fisheep.cc:5000/ubuntu:20.04


# 4 查看registry仓库中的镜像列表
# 结果格式：{"repositories":["ubuntu"]}
curl http://fisheep.cc:5000/v2/_catalog

# 5 查看registry仓库中指定镜像(ubuntu)的标签列表
# 结果格式：{"name":"ubuntu","tags":["20.04"]}
curl http://fisheep.cc:5000/v2/ubuntu/tags/list
```

#### 问题记录

##### 1 拉取/推送镜像失败

错误提示：
> ```bash
> ian@ubuntu:~$ docker pull fisheep.cc:5000/ubuntu:20.04
> Error response from daemon: Get https://fisheep.cc:5000/v2/: http: server gave HTTP response to HTTPS client
> ```

解决方法：
```bash
sudo vim /etc/docker/damon.json
sudo systemctl restart docker
```

其中，damon.json增加如下内容
```json
{"insecure-registries": ["fisheep.cc:5000"]}
```

