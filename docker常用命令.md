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
docker run -d -p 8080:8080 --net=host -v /usr/local/dorker/schedule/logs/:/usr/local/dorker/schedule/logs/ --name tg_schedule schedule
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
安装 portainer

docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart always -v \\.\pipe\docker_engine:\\.\pipe\docker_engine -v portainer_data:C:\docker\portainer\data\ portainer/portainer-ce:latest
