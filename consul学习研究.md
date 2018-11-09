# 1.1	consul安装部署
## 第一步：下载
wget https://releases.hashicorp.com/consul/0.7.5/consul_0.7.5_linux_amd64.zip
## 第二步：解压
unzip consul_0.7.5_linux_amd64.zip
## 第三步：安装
./consul
## 出现如下信息，说明安装成功：
  ![image](https://github.com/xfgeng666/Apollo/blob/master/images/20181109094705.png)
## 第四步：启动
./consul agent -dev -ui -node=consul-dev -client=10.4.149.132
## 出现如下信息，说明启动成功：
  ![image](https://github.com/xfgeng666/Apollo/blob/master/images/20181109103125.png)
然后浏览器访问：http://10.4.149.132:8500
 ![image](https://github.com/xfgeng666/Apollo/blob/master/images/20181109103153.png)
