## 启动docker服务
```shell
systemctl start docker
```

## 创建镜像
```shell
docker build -t [镜像名称:版本] [路径]
```

### 创建实例
```shell
#centos
docker run -d -p 8080:8080 -v /usr/local/dorker/schedule/logs/:/usr/local/dorker/schedule/logs/ --name tg_schedule schedule
```

### 启动、停止、删除实例
```shell
docker start [NAMES]
docker stop [NAMES]
docker rm -f [NAMES]
```

### 查看运行实例、查看所有实例
```shell
docker ps
docker ps -a
```

### 查看所有镜像、删除镜像
```shell
docker images
docker rmi [IMAGE ID]
```

### 镜像导出、导入
```shell
docker save ubuntu:latest > ubuntu.tar
docker load -i jackpan_dragonwell8_v_8.11.12.tar
```

### 进入虚拟机命令行
```shell
docker exec -it [CONTAINER ID] bash
```

### 安装 portainer
```shell

docker volume create portainer_data

#linux
docker run -d -p 8000:8000 -p 9000:9000 --restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v portainer_data:/data \
--name portainer portainer/portainer-ce:latest

#window
docker run -d -p 8000:8000 -p 9000:9000 --restart=always `
-v /var/run/docker.sock:/var/run/docker.sock `
-v portainer_data:/data `
--name portainer portainer/portainer-ce:latest

```

### 安装 registry 私有库
* -e REGISTRY_STORAGE_DELETE_ENABLED="true" 是支持删除
```shell

#linxu 
docker run -itd -p 5000:5000 --restart=always \
-v /host_mnt/d/docker/registry/:/var/lib/registry \
-e REGISTRY_STORAGE_DELETE_ENABLED="true" \
--name registry registry:latest

#自定义配置
docker run -itd -p 5000:5000 --restart=always \
-v /home/registry/:/var/lib/registry \
-v /home/registry/config.yml:/etc/docker/registry/config.yml \
-e REGISTRY_STORAGE_DELETE_ENABLED="true" \
--name registry registry:latest

#window
docker run -itd -p 5000:5000 --restart=always `
-v /host_mnt/d/docker/registry/:/var/lib/registry `
-e REGISTRY_STORAGE_DELETE_ENABLED="true" `
--name registry registry:latest

#自定义配置
docker run -itd -p 5000:5000 --restart=always `
-v /host_mnt/d/docker/registry/:/var/lib/registry `
-v /host_mnt/d/docker/registry/config.yml:/etc/docker/registry/config.yml `
-e REGISTRY_STORAGE_DELETE_ENABLED="true" `
--name registry registry:latest
```

### 安装私有库UI docker-registry-ui
* 要么安装joxit/docker-registry-ui:static版本
* 安装最新版本joxit/docker-registry-ui:latest,需要修改registry容器的/etc/docker/registry/config.yml文件<br/>
在http: headers: 下加上 Access-Control-Allow-Origin: ['*'],否则会报Access-control-allow-origin错误

```shell

# linux
# latest版本
docker run -p 8280:80 --name registry-ui \
--link registry:registry \
-e REGISTRY_URL="http://192.168.0.6:5000" \
-e DELETE_IMAGES="true" \
-e REGISTRY_TITLE="Registry" \
-d joxit/docker-registry-ui:latest

# static版本
docker run -p 8280:80 --name registry-ui `
--link registry:registry `
-e REGISTRY_URL="http://192.168.0.2:5000" `
-e DELETE_IMAGES="true" `
-e REGISTRY_TITLE="Registry" `
-d joxit/docker-registry-ui:static

# latest版本
docker run -p 8280:80 --name registry-ui `
--link registry:registry `
-e REGISTRY_URL="http://192.168.0.2:5000" `
-e DELETE_IMAGES="true" `
-e REGISTRY_TITLE="Registry" `
-d joxit/docker-registry-ui:latest
```

#### 安装 nginx
```shell
#window
docker run -d -p 80:80 -p 443:443 `
-e TZ=Asia/Shanghai `
-v /host_mnt/d/docker/nginx/conf/:/etc/nginx/conf.d/ `
-v /host_mnt/d/docker/nginx/logs/:/var/log/nginx/ `
--name nginx nginx
```

#### 安装 tengine
```shell
#linxu
docker run -d -p 80:80 -p 443:443 \
-e TZ=Asia/Shanghai \
-v /home/nginx/logs/:/var/log/nginx/ \
-v /home/nginx/nginx.conf:/etc/nginx/nginx.conf \
-v /home/nginx/conf/:/etc/nginx/conf.d/ \
-v /home/nginx/html/:/etc/nginx/html/ \
--name tengine infralibrary/tengine

#window
docker run -d -p 80:80 -p 443:443 `
-e TZ=Asia/Shanghai `
-v /host_mnt/d/docker/nginx/logs/:/var/log/nginx/ `
-v /host_mnt/d/docker/nginx/nginx.conf:/etc/nginx/nginx.conf `
-v /host_mnt/d/docker/nginx/conf/:/etc/nginx/conf.d/ `
-v /host_mnt/d/docker/nginx/html/:/etc/nginx/html/ `
--name tengine infralibrary/tengine
```

#### 安装 mongodb
```shell
#linxu
docker run -d -p 27017:27017 \
-v /home/mongo/data/:/data/db/ \
-v /home/mongo/mongo.conf:/etc/mongo.conf \
-v /home/mongo/mongo.log:/data/mongo.log \
--name mongo mongo:latest --config /etc/mongo.conf --auth
```
mongo.conf
```yml
storage:
  dbPath: /data/db/
  journal:
    enabled: true
systemLog:
  destination: file
  logAppend: true
  path: /data/mongo.log
net:
  port: 27017
  bindIp: 0.0.0.0
```

* mongo.log必须要先创建，开启可读权限

#### mongodb开启单节点分片,事务支持
* 开启单节点分片，不能先开启--auth，在创建完用户后在开启auth。报(BadValue: security.keyFile is required when authorization is enabled with replica sets)错误

1.先创建mongodb容器。
```shell
#linxu
docker run -d -p 27017:27017 \
-v /home/mongo/data/:/data/db/ \
-v /home/mongo/mongo.conf:/etc/mongo.conf \
-v /home/mongo/mongo.log:/data/mongo.log \
--name mongo mongo:latest --config /etc/mongo.conf
```
mongo.conf
```yml
storage:
  dbPath: /data/db/
  journal:
    enabled: true
systemLog:
  destination: file
  logAppend: true
  path: /data/mongo.log
net:
  port: 27017
  bindIp: 0.0.0.0
  #开启分片
replication:
  replSetName: rs0  
```

2.在进入mongodb创建分片,在创建用户。
```
docker exec -it mongo mongo admin

rs.initiate({_id:"rs0",members:[{_id:0,host:"127.0.0.1:27017",priority:1}]})

use admin;

db.createUser({
	user: "admin",
	pwd: "admin",
	roles: [{
		role: "root",
		db: "admin"
	}]
})

```

3.停止docker服务。
systemctl stop docker

4.开启auth。
进入 /var/lib/docker/containers/目录下找到对应的容器目录在进入，编辑config.v2.json

5.启动docker服务
systemctl start docker
