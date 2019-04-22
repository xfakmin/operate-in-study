# kafka 安装  

## 安装 jdk  

kafka 运行依赖 jdk，需要先安装 jdk;  

`sudo apt install default-jdk`  

## 下载 kafka 程序包  

从官网上下载 kafka 的程序包  

`wget http://mirrors.tuna.tsinghua.edu.cn/apache/kafka/2.2.0/kafka_2.11-2.2.0.tgz`  

下载下来后时一个 tgz 文件;  

## 解压文件  

`tar -xzf kafka_2.11-2.2.0.tgz`  

解压之后，就可以运行 kafka 程序了。  

- 运行 zookeeper 程序  

`./zookeeper-server-start.sh ../config/zookeeper.properties`  

先执行 zookeeper 程序  

- 运行 kafka 程序  

`./kafka-server-start.sh ../config/server.properties`  

> 不需要单独下载 zookeeper 程序;  
> 使用的时默认的配置数据连接的 kafka 程序，用于测试，正式的服务，需要配置合适的参数。  

