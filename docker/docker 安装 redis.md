## docker 安装 redis  

### 下载 redis 镜像  

`docker pull redis:3.2`  

> 目前项目中使用的 redis 3.2 版本的，故没有下载最新版本的数据。  

### 运行 redis 容器  

`docker run --name redis -p 6379:6379 -v $PWD/redis_data:/data -d redis:3.2 redis-server --appendonly yes`  

> -p 将容器的 6379 端口映射到本机的 6379 端口;  
> -v 将本机的当前目录的 redis_data 挂载到容器的 /data 目录;  

### 链接 redis 容器  

`docker exec -it redis redis-cli`  

> redis 默认的端口就是 6379 端口;  

### 使用配置文件启动 docker 容器  

`docker run -v $PWD/redis-master.conf:/usr/local/etc/redis/redis.conf --name redis-master -d redis:3.2 redis-server /usr/local/etc/redis/redis.conf`  

> 注意下载对应版本的 redis.conf 文件， 高版本的配置文件中可能有些新参数导致启动失败;  
> 使用 redis.conf 配置文件启动的时候，是不可以将参数 `daemonize` 设置为 yes 状态;  

### 启动集群  

```shell  
# 启动主
docker run -v $PWD/redis-master.conf:/usr/local/etc/redis/redis.conf --name redis-master -d redis:3.2 redis-server /usr/local/etc/redis/redis.conf  

# 启动从服务器  
docker run -v $PWD/redis-slave1.conf:/usr/local/etc/redis/redis.conf --name redis-slave1 --link redis-master:master -d redis:3.2 redis-server /usr/local/etc/redis/redis.conf
```

> 配置从服务器的时候，需要修改配置文件，将 slaveof 的注释打开，并配置主服务器的host或者IP;  
> 这里使用 --link 参数，链接两个容器，并使用 master 标识 redis-master 容器的ip;  

* 从服务器的配置文件修改  

`slaveof master 6379`  

* 启动容器之后，可以进入容器中，然后使用 redis-cli 链接 redis 服务器，info 命令可以查看主从配置的链接数，如果有问题的话，需要改配置文件;  

`bind 0.0.0.0`  



