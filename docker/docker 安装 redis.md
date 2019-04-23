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

