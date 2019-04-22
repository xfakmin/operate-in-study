# docker 安装 mysql  

## 下载 mysql  

`docker pull mysql:5.7`  

下载指定的版本比较好，当前默认的下载的 `laster` 版本时 mysql8 , 使用 `mycli` 连接数据库会有报错，连不上数据库;  
## 运行 mysql 镜像  

`docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=meixihua -d mysql:5.7`  

- -p 指定端口映射;  
- --name 指定容器的名称;  
- -e 指定容器中的环境变量;  
- -d 表示后台执行;  

> 当运行起来后，立即使用 mycli 连接数据库容器是有可能产生错误的。稍等一下就可以了。  

`docker run -p 3306:3306 --name mymysql -v $PWD/conf:/etc/mysql/conf.d -v $PWD/logs:/logs -v $PWD/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.6`  

- -p 3306:3306：将容器的 3306 端口映射到主机的 3306 端口。  
- -v -v $PWD/conf:/etc/mysql/conf.d：将主机当前目录下的 conf/my.cnf 挂载到容器的 /etc/mysql/my.cnf。
- -v $PWD/logs:/logs：将主机当前目录下的 logs 目录挂载到容器的 /logs。  
- -v $PWD/data:/var/lib/mysql ：将主机当前目录下的data目录挂载到容器的 /var/lib/mysql 。  
- -e MYSQL_ROOT_PASSWORD=123456：初始化 root 用户的密码。  

> 镜像相关的信息需要到镜像官网中看。  
> 默认的 `mysql` 的配置文件是在 `/etc/mysql/conf.d` ;
> 镜像默认的 logs 文件在 /logs ;  
> mysql 的配置文件采用的时 toml 格式的文件。  

