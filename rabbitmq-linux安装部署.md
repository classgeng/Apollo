# 一、安装依赖
```
yum install gcc
yum install pcre-devel
yum install zlib zlib-devel
yum install openssl openssl-devel
yum install ncurses-devel
一键安装上面五个依赖
yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel ncurses-devel
```
# 二、安装Erlang环境
```
wget http://erlang.org/download/otp_src_18.2.1.tar.gz
tar xvfz otp_src_18.2.1.tar.gz 
./configure 
make install
```
# 三、安装RabbitMQ
```
wget http://www.rabbitmq.com/releases/rabbitmq-server/v3.6.9/rabbitmq-server-generic-unix-3.6.9.tar.xz
tar -xvf rabbitmq-server-generic-unix-3.6.9.tar.xz
cd rabbitmq_server-3.6.9/
vim /etc/profile
RABBITMQ_HOME=/usr/local/rabbitmq_server-3.6.9
export PATH=$RABBITMQ_HOME/sbin:$PATH   
source /etc/profile
rabbitMQ安装成功。
```

## 启用MQ管理方式
```
rabbitmq-plugins enable rabbitmq_management
```
# 四、RabbitMQ常用命令
```
查看服务状态：rabbitmqctl status
关闭服务：rabbitmqctl stop
查看mq用户：rabbitmqctl list_users  
查看用户权限：rabbitmqctl list_user_permissions guest
新增用户： rabbitmqctl add_user admin 123456
赋予管理员权限：
rabbitmqctl set_user_tags admin administrator 
rabbitmqctl set_permissions -p "/" admin ".*" ".*" ".*" 
```
