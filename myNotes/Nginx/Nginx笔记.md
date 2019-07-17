# Nginx笔记

1. 安装过程（源码编译安装）：
	1. 下载源码
	2. 安装依赖的环境(注意同时安装devel开发包)
		1. gcc环境：nginx为C语言编写。从官网下载的nginx源码编译依赖gcc环境。
		2. PCRE(Perl Compatible Regular Expressions)：PCRE是一个Perl库，nginx的http模块使用pcre来解析正则表达式。
		3. zlib：zlib库提供了很多种压缩和解压缩的方式，nginx使用zlib对http包的内容进行gzip。
		4. OpenSSL：nginx使用HTTPS需要使用openssl。
	3. 进入源码目录，运行configure，具体如下：
	```./configure  --prefix=/usr/local/nginx --pid-path=/var/run/nginx/nginx.pid --lock-path=/var/lock/nginx.lock --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-http_gzip_static_module --http-client-body-temp-path=/var/temp/nginx/client --http-proxy-temp-path=/var/temp/nginx/proxy --http-fastcgi-temp-path=/var/temp/nginx/fastcgi --http-uwsgi-temp-path=/var/temp/nginx/uwsgi --http-scgi-temp-path=/var/temp/nginx/scgi --with-http_ssl_module```。各个配置的具体含义参考官网。
	4. 编译安装1. ```make```,2. ```make  install```
	5. 常用命令
    	- ```nginx -c /usr/local/nginx/conf/nginx.conf```  启动nginx(windows下start nginx);  
    	- ```nginx -s quit```       停止ngix  
    	- ```nginx -s reload```     重新载入nginx(当配置信息发生修改时)  
    	- ```nginx -s reopen```     打开日志文件  
    	- ```nginx -v```            查看版本  
    	- ```nginx -t```            查看nginx的配置文件的目录  
    	- ```nginx -h```           查看帮助信息
