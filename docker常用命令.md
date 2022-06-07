#### 启动docker服务
```shell
systemctl start docker
```

#### 创建镜像
```shell
docker build -t [镜像名称] [路径]
```

#### 创建实例
```shell
#centos
docker run -d -p 8080:8080 --net=host -v /usr/local/dorker/schedule/logs/:/usr/local/dorker/schedule/logs/ --name tg_schedule schedule
#window
docker run -d -p 8080:8080 --net=bridge -v /host_mnt/d/docker/schedule/logs/:/usr/local/dorker/schedule/logs/ --name tg_schedule schedule
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
docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /host_mnt/d/docker/portainer_data/:/data portainer/portainer-ce:latest
```

#### 安装 私有库
```shell

docker run -itd -v /host_mnt/d/docker/registry/:/var/lib/registry -p 5000:5000 --restart=always --name registry registry:latest

#支持删除
docker run -itd -v /host_mnt/d/docker/registry/:/var/lib/registry -p 5000:5000 --restart=always -e REGISTRY_STORAGE_DELETE_ENABLED="true" --name registry registry:latest

```

#### 安装 nginx
```shell
docker run -d -p 80:80 -p 443:443 -v /host_mnt/d/docker/nginx/conf/:/etc/nginx/conf.d/ -v /host_mnt/d/docker/nginx/logs/:/var/log/nginx/ --name nginx  nginx
```

