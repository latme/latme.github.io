
### Docker Registry

> 官网：
> - [joxit.dev/docker-registry-ui](https://joxit.dev/docker-registry-ui)


#### 安装使用

##### 服务端启动服务

```bash
# 1 拉取registry-ui镜像
docker pull joxit/docker-registry-ui:1.5-static

# 2 创建docker容器
docker run  -d \
            -v /srv/run/dockerreg:/var/lib/registry \
            -p 5100:80 \
            -e REGISTRY_TITLE="Registry2" \
            -e REGISTRY_URL="http://fisheep.cc:5000" \
            -e DELETE_IMAGES="true" \
            --link=registry-demo:registry2 \
            --name=registry-ui \
            --restart=always \
            joxit/docker-registry-ui:1.5-static

# 其中，REGISTRY_TITLE/REGISTRY_URL显示使用，--link才是真正与registry仓库对接的。
```

##### 客户端（浏览器）使用

```bash
http://fisheep.cc:5100
```

#### 问题记录

##### 1 删除镜像失败

错误提示：
> ```
> {"errors":[{"code":"UNSUPPORTED","message":"The operation is unsupported."}]}
> ```

错误原因：
docker registry默认不允许删除镜像。

**解决方法（已创建的registry）：**
```bash
# 进入docker容器
docker exec -it registry-demo /bin/sh

# 修改配置文件
vi /etc/docker/registry/config.yml

# 退出docker容器
exit

# 重启docker容器
docker restart registry-demo
```

其中，config.yml增加如下内容
```yml
storage:
  delete:
    enabled: true
```

**解决方法（新创建的registry）：**
```bash
# 创建docker容器时，指定下面的环境变量
-e REGISTRY_STORAGE_DELETE_ENABLED=true
```

