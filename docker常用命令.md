#### 启动docker服务
```shell
systemctl start docker
```

#### 创建镜像
```shell
docker build -t [镜像名称:版本] [路径]
```

#### 创建实例
```shell
#centos
docker run -d -p 8080:8080 -v /usr/local/dorker/schedule/logs/:/usr/local/dorker/schedule/logs/ --name tg_schedule schedule
```

#### 启动、停止、删除实例
```shell
docker start [NAMES]
docker stop [NAMES]
docker rm -f [NAMES]
```

#### 查看运行实例、查看所有实例
```shell
docker ps
docker ps -a
```

#### 查看所有镜像、删除镜像
```shell
docker images
docker rmi [IMAGE ID]
```

#### 镜像导出、导入
```shell
docker save ubuntu:latest > ubuntu.tar
docker load -i jackpan_dragonwell8_v_8.11.12.tar
```

#### 进入虚拟机命令行
```shell
docker exec -it [CONTAINER ID] bash
```

#### 安装 portainer
```shell
docker run -d -p 8000:8000 -p 9000:9000 --restart=always `
-v /var/run/docker.sock:/var/run/docker.sock `
-v /host_mnt/d/docker/portainer_data/:/data `
--name portainer portainer/portainer-ce:latest
```

#### 安装 registry 私有库
```shell

docker run -itd -p 5000:5000 --restart=always `
-v /host_mnt/d/docker/registry/:/var/lib/registry `
--name registry registry:latest

# 支持删除
docker run -itd -p 5000:5000 --restart=always `
-v /host_mnt/d/docker/registry/:/var/lib/registry `
-e REGISTRY_STORAGE_DELETE_ENABLED="true" `
--name registry registry:lates

# 支持私有库UI
docker run -p 8280:80 --name registry-ui `
--link registry:registry `
-e REGISTRY_URL="http://192.168.0.2:5000" `
-e DELETE_IMAGES="true" `
-e REGISTRY_TITLE="Registry" `
-d joxit/docker-registry-ui:static

```

#### 安装 nginx
```shell
docker run -d -p 80:80 -p 443:443 `
-e TZ=Asia/Shanghai `
-v /host_mnt/d/docker/nginx/conf/:/etc/nginx/conf.d/ `
-v /host_mnt/d/docker/nginx/logs/:/var/log/nginx/ `
--name nginx nginx
```

#### 安装 tengine
```shell
docker run -d -p 80:80 -p 443:443 `
-e TZ=Asia/Shanghai `
-v /host_mnt/d/docker/nginx/logs/:/var/log/nginx/ `
-v /host_mnt/d/docker/nginx/nginx.conf:/etc/nginx/nginx.conf `
-v /host_mnt/d/docker/nginx/conf/:/etc/nginx/conf.d/ `
-v /host_mnt/d/docker/nginx/html/:/usr/share/nginx/html/ `
--name tengine infralibrary/tengine
```
