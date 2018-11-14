# 下载
wget http://nginx.org/download/nginx-1.14.0.tar.gz
# 加压
tar -zxvf nginx-1.1.10.tar.gz
# 安装
cd nginx-1.1.10  
./configure  
make  
make install  
# 启动
启动：/usr/local/nginx/sbin/nginx -c /usr/local/nginx/nginx-1.14.0/conf/nginx.conf  
重启：/usr/local/nginx/sbin/nginx -s reload
# 停止
从容停止Nginx：kill -QUIT 主进程号，例如：kill -QUIT 16391   
快速停止Nginx：kill -TERM 主进程号  
强制停止Nginx：kill -9 主进程号  
