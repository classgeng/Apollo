# zookeeper linux环境安装部署
## 一、单节点部署
### 第一步：下载
wget https://mirrors.tuna.tsinghua.edu.cn/apache/zookeeper/zookeeper-3.4.10/zookeeper-3.4.10.tar.gz
### 第二步：解压
tar -xvf zookeeper-3.4.10.tar.gz
### 第三步：新建目录
cd /usr/local/zookeeper-3.4.10  
mkdir data logs
### 第四步：修改配置
cd /usr/local/zookeeper-3.4.10/conf  
cp zoo_sample.cfg zoo.cfg  
vim zoo.cfg  
修改内容：  
#数据文件夹  
dataDir=/usr/local/zookeeper-3.4.10/data  
#日志文件夹  
dataLogDir=/usr/local/zookeeper-3.4.10/logs  
#客户端访问的端口号  
clientPort=2181  
### 第五步：启动服务
cd /usr/local/zookeeper-3.4.10/bin  
启动 sh zkServer.sh start  
    如打印如下信息则表明启动成功：  
    ZooKeeper JMX enabled by default  
    Using config: /usr/local/services/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg  
    Starting zookeeper ... STARTED  
重启 sh zkServer.sh restart  
    如打印如下信息则表明重启成功：  
    ZooKeeper JMX enabled by default  
    Using config: /usr/local/services/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg  
    ZooKeeper JMX enabled by default  
    Using config: /usr/local/services/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg  
    Stopping zookeeper ... STOPPED  
    ZooKeeper JMX enabled by default  
    Using config: /usr/local/services/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg  
    Starting zookeeper ... STARTED  
    
