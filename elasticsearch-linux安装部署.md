# 下载
```
cd /usr/local
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.6.3.tar.gz
```
# 解压安装
```
tar -xvf elasticsearch-5.6.3.tar.gz
mv elasticsearch-5.6.3 elasticsearch
```
# 创建数据路径和日志文件路径
```
cd elasticsearch
mkdir data logs
```
# 修改配置
```
cd config
vim elasticsearch.yml
```
## 单节点配置
```
cluster.name: cluster-es  	# 集群名
node.name: node-1			# 节点名
path.data: /usr/local/elasticsearch/data		# index数据路径 
path.logs: /usr/local/elasticsearch/logs  	# 日志文件路径
network.host: 0.0.0.0			# 主机IP 
http.port: 9200				# 端口
```
## 集群配置
```
集群配置，在单节点基础上要配置Cluster，Node，Discovery三个块的配置。
```
# 创建esuser用户(root用户不能启动elasticsearch)
```
groupadd esgroup  # 创建用户组
useradd esuser -g esgroup -p 123456 # 创建用户并指定用户组以及设置密码
chown -R esuser:esgroup elasticsearch # 更改elasticsearch文件夹及内部文件的所属用户及组为esuser:esgroup
```
# 启动
```
su esuser #切换用户
cd /usr/local/elasticsearch/bin
./elasticsearch
./elasticsearch -d  #后台启动
```
### 启动报错解决
```
1，[1]: max file descriptors [4096] for elasticsearch process is too low, increase to at least [65536] 
意思是说你的进程不够用了。
解决方案： 切到root 用户：进入到security目录下的limits.conf；
执行命令 vim /etc/security/limits.conf 在文件的末尾添加下面的参数值：
soft nofile 65536
hard nofile 131072
soft nproc 2048
hard nproc 4096
前面的*符号必须带上，然后重新启动就可以了。
执行完成后可以使用命令 ulimit -n 查看进程数 。

2，[2]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144] 
需要修改系统变量的最大值
解决方案：切换到root用户，修改配置/etc/sysctl.conf 
增加配置值： vm.max_map_count=655360
执行命令 sysctl -p 这样就可以了。
然后重新启动ES服务 就可以了。
```
# 验证
http://ip:9200 
# 安装elasticsearch-head插件

