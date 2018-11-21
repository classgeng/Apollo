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
## 下载
```
wget https://github.com/mobz/elasticsearch-head/archive/master.zip
```
## 解压安装
```
unzip master.zip
cd elasticsearch-head-master
```
### 安装node
于head插件本质上还是一个nodejs的工程，因此需要安装node，使用npm来安装依赖的包 可以去官网下载https://nodejs.org/en/download/安装包安装。 
我投简单是直接用yum命令安装。 
```
curl -sL https://rpm.nodesource.com/setup_8.x | bash -
yum install -y nodejs
```
### 安装grunt 
grunt是一个很方便的构建工具，可以进行打包压缩、测试、执行等等的工作，5.6里的head插件就是通过grunt启动的。因此需要安装一下grunt：
```
cd elasticsearch-head-master
npm install -g grunt-cli  //执行后会生成node_modules文件夹
npm install
```
## 修改配置
5.0以上，elasticsearch-head 不能放在elasticsearch的 plugins、modules 目录下，否则elasticsearch启动会报错
### 修改vim Gruntfile.js文件：增加hostname属性，设置为*
```
connect: {
    server: {
        options: {
            port: 9100,
            hostname: '*',
            base: '.',
            keepalive: true
        }
    }
}
```
### 修改 vim _site/app.js 文件
修改head的连接地址:   
this.base_uri = this.config.base_uri || this.prefs.get(“app-base_uri”) || “http://localhost:9200“;   
修改成ElasticSearch的机器地址   
this.base_uri = this.config.base_uri || this.prefs.get(“app-base_uri”) || “http://192.168.0.153:9200“;

## 启动
修改完成你就可以启动head插件了：在 elasticsearch-head-master下启动服务
```
cd elasticsearch-head-master
grunt server &  #后台启动
```
## 验证
访问地址：http://192.168.0.153:9100 
如果你在浏览器中访问不了，请检查防火墙是否关闭。 

# 参考地址
https://blog.csdn.net/chenxun_2010/article/details/78437852


