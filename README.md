# nginx 1.2.0 编译过程
*  官网: Documentation is available at http://nginx.org


## 1)安装git

```
yum -y install git

[root@localhost ~]# git --version
git version 1.8.3.1
```

## 2)clone项目

```
git clone git clone https://github.com/132982jianan/nginx-1.2.0.git

或者从官网下载并解压项目
  wget http://nginx.org/download/nginx-1.2.0.tar.gz
  tar xvf nginx-1.2.0.tar.gz
```

## 3)gcc安装
```
yum install -y gcc
```

## 4)3个步骤：

```
bash ./configure --prefix=/usr/jn
make
make install
```

## 5)

```
如果报错就按照提示安装需要的2个包：
    yum install -y  pcre-devel
    yum install -y zlib-devel
```

## 6)编译失败提示

```
checking for system md5 library ... not found
checking for OpenSSL md5 crypto library ... not found
checking for sha1 in system md library ... not found
checking for OpenSSL sha1 crypto library ... not found
checking for zlib library ... not found

./configure: error: the HTTP gzip module requires the zlib library.
You can either disable the module by using --without-http_gzip_module
option, or install the zlib library into the system, or build the zlib library
statically from the source with nginx by using --with-zlib=<path> option.
```

## 7)编译成功提示
```
Configuration summary
  + using system PCRE library
  + OpenSSL library is not used
  + using builtin md5 code
  + sha1 library is not found
  + using system zlib library

  nginx path prefix: "/usr/jn"
  nginx binary file: "/usr/jn/sbin/nginx"
  nginx configuration prefix: "/usr/jn/conf"
  nginx configuration file: "/usr/jn/conf/nginx.conf"
  nginx pid file: "/usr/jn/logs/nginx.pid"
  nginx error log file: "/usr/jn/logs/error.log"
  nginx http access log file: "/usr/jn/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"

  
objs/ngx_modules.o \
-lpthread -lcrypt -lpcre -lz
make[1]: Leaving directory `/mnt/nginx-1.2.0'
make -f objs/Makefile manpage
make[1]: Entering directory `/mnt/nginx-1.2.0'
sed -e "s|%%PREFIX%%|/usr/jn|" \
	-e "s|%%PID_PATH%%|/usr/jn/logs/nginx.pid|" \
	-e "s|%%CONF_PATH%%|/usr/jn/conf/nginx.conf|" \
	-e "s|%%ERROR_LOG_PATH%%|/usr/jn/logs/error.log|" \
	< man/nginx.8 > objs/nginx.8
make[1]: Leaving directory `/mnt/nginx-1.2.0'


cp conf/nginx.conf '/usr/jn/conf/nginx.conf.default'
test -d '/usr/jn/logs' 		|| mkdir -p '/usr/jn/logs'
test -d '/usr/jn/logs' || 		mkdir -p '/usr/jn/logs'
test -d '/usr/jn/html' 		|| cp -R html '/usr/jn'
test -d '/usr/jn/logs' || 		mkdir -p '/usr/jn/logs'
make[1]: Leaving directory `/mnt/nginx-1.2.0'
```

## 8)启动编译后的nginx

```
[root@localhost nginx-1.2.0]# ./objs/nginx -c /usr/l
lib/     lib64/   libexec/ local/   
[root@localhost nginx-1.2.0]# ./objs/nginx -c ./conf/nginx.conf 
[root@localhost nginx-1.2.0]# ./objs/nginx -c ./conf/nginx.conf 
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] still could not bind()
```



