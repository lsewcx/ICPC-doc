# 运维

## nginx 介绍

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310151159875.png)

## 宝塔linux

## [宝塔面板下载，免费全能的服务器运维软件 (bt.cn)](https://www.bt.cn/new/download.html)

## 在线自动生成nginx配置文件

https://www.digitalocean.com/community/tools/nginx?global.app.lang=zhCN

可以自由选择所需的应用，生成nginx配置作为参考。

```
根据你的业务需求，自动生成复杂的nginx配置文件，提供你作为参考，非常好用
```

## nginx企业用它干啥

```
1.提供静态页面展示，网页服务  
2.提供多个网站、多个域名的网页服务
====================================================


3.提供反向代理服务（结合动态应用程序）

4.提供简单资源下载服务（密码认证） ftp服务


5.用户行为分析（日志功能）



```

## nginx的运行架构

```
nginx运行后，有多少个干活的工人，多进程，调用多个cpu去解析用户的请求

在linux中进行多进程开发，开辟多个进程，调用多个cpu，当然也会消耗更多的机器资源，内存，cpu资源，给服务器带来更大的压力
- 不是说进程越多，干活越快，合理的分配，才能达到最高效的处理效率

=====
有一个屋子要装修，请1个工人干活，还是请5个工人干活，请500个工人干活

哪一个效率是最高的呢？ 最合适的？
===
关于nginx的优化设置，nginx默认应该启动多少个进程去工作呢？
默认就是根据cpu的核数去设置进程数即可。

=======

```

## master进程

包工头进程，管理nginx的数据，创建worker工作进程。

```
1.启动时检查nginx.conf是否正确，语法错误；
2.根据配置文件的参数创建、且监控worker进程的数量和状态；
3.监听socket，接收client发起的请求，然后worker竞争抢夺链接，获胜的可以处理且响应请求。
4.接收运维超哥发送的管理nginx进程的信号，并且将信号通知到worker进程。
5.如果运维超哥发送了reload命令，则读取新配置文件，创建新的worker进程，结束旧的worker进程。
```

## nginx处理http请求流程

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310151201785.png)

## nginx安装实践

```
利用nginx -V  命令可以看到当前操作的这个命令二进制命令，详细的信息，包括支持了哪些模块

```

## nginx的安装形式

* docker安装
* 源代码编译安装，优点
  * 版本，可以获取官网最新的软件包，甚至最新测试版，都可以直接编译安装
  * 还有稳定版本
  * 自由定义，安装路径自由定义，
  * 自由定义第三方插件
  * 缺点，安装步骤繁琐，耗时太长，看你要装多少个模块，编译添加的模块多，安装的就更久
* rpm安装
  * 得提前准备好nginx本身的rpm包，以及相关依赖的rpm包
  * 用于离线安装nginx的环境
* yum安装，你会用哪些形式的仓库？
  * 阿里云第三方仓库（centos-base.repo,epel.repo）
    * 这个其实都不靠谱。
  * 自建yum仓库（得提前准备好nginx本身的rpm包，以及相关依赖的rpm包）
  * nginx官网仓库（获取官网最新稳定版的yum源仓库）
    * yum一键安装，省心省事，版本也是有一定的保障的，rpm的安全性也是有保障的

```
官网yum仓库
源代码编译
离线的rpm安装（yum 自建仓库）
```

## 编译安装

## yum安装

```
1. 配置官网yum源，一键安装即可

cat > /etc/yum.repos.d/nginx.repo << 'EOF'
[nginx-stable]
name=nginx stable repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key
EOF

2.清空yum源，安装最新版nginx
[root@web-8 /etc/yum.repos.d]#yum clean all

[root@web-8 /etc/yum.repos.d]#yum install nginx -y

3.查看PATH变量
[root@web-8 /etc/yum.repos.d]#which nginx
/usr/sbin/nginx
[root@web-8 /etc/yum.repos.d]#ll /usr/sbin/nginx
-rwxr-xr-x 1 root root 1377720 Nov 16  2021 /usr/sbin/nginx


[root@web-8 /etc/yum.repos.d]#nginx -V
nginx version: nginx/1.20.2
built by gcc 4.8.5 20150623 (Red Hat 4.8.5-44) (GCC) 
built with OpenSSL 1.0.2k-fips  26 Jan 2017
TLS SNI support enabled
configure arguments: --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib64/nginx/modules --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx --group=nginx --with-compat --with-file-aio --with-threads --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-mail --with-mail_ssl_module --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module --with-cc-opt='-O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches -m64 -mtune=generic -fPIC' --with-ld-opt='-Wl,-z,relro -Wl,-z,now -pie'


```

## nginx管理命令

```
nginx -t  # 检测nginx.conf语法
nginx -s  reload  # 重新读取nginx.conf
nginx -s stop   # 停止nginx  kill -15 nginx

nginx  # 默认是直接运行，前提是当前机器没运行nginx

#你通过yum安装的nginx请你用systemctl去管理


# 不能多次执行nginx二进制命令
[root@web-8 ~]#
[root@web-8 ~]#nginx
[root@web-8 ~]#nginx # 会报错


# nginx -s reload ,会发生什么

nginx -s reload是给master进程发信号，重新读取配置信息，导致worker重新生成，因此worker-pid发生了变化

但是master进程id不带变化的（包工头，一直没变，更换了手底下的干活的工人）
================================
配置文件变化，就好比 合同变化了（包工头还是他，但是工人更换了一批）



===========
只有你restart的时候，包工头，也会被更换

你只能先停止， 再重启
nginx -s stop # 不会报错的

==============================

如果出现如下错误，如何解决，其实是通过pid，管理nginx的进程
 ~]#nginx -s stop
nginx: [error] invalid PID number "" in "/var/run/nginx.pid"
[root@web-8 ~]#
[root@web-8 ~]#
[root@web-8 ~]#cat /var/run/nginx.pid
[root@web-8 ~]#
[root@web-8 ~]#
[root@web-8 ~]#
[root@web-8 ~]#ps -ef |grep nginx
root       3599      1  0 16:10 ?        00:00:00 nginx: master process nginx
nginx      3628   3599  0 16:12 ?        00:00:00 nginx: worker process
root       3677   3434  0 16:19 pts/0    00:00:00 grep --color=auto nginx
[root@web-8 ~]#
[root@web-8 ~]#
[root@web-8 ~]#echo 3599 > /var/run/nginx.pid 
[root@web-8 ~]#
[root@web-8 ~]#
[root@web-8 ~]#nginx -s stop
[root@web-8 ~]#
[root@web-8 ~]#
[root@web-8 ~]#!ps
ps -ef |grep nginx
root       3686   3434  0 16:19 pts/0    00:00:00 grep --color=auto nginx
[root@web-8 ~]#
[root@web-8 ~]#
[root@web-8 ~]## 看懂了扣 6 不懂7 
[root@web-8 ~]#



# 明确，现在用systemctl去管理nginx了
[root@web-8 ~]#systemctl start nginx


查看状态，reload， restart nginx，查看进程id号

[root@web-8 ~]#systemctl status nginx

[root@web-8 ~]#systemctl reload nginx  # worker变化，master不变

[root@web-8 ~]#systemctl restart nginx  # 整个nginx进程变化

# 用什么命令启动的，就用什么方式去管理该进程
```

## nginx配置文件详解

```
安装完了之后，后续nginx的所有功能，都是围绕着修改nginx配置文件生效了

看懂配置文件，运维来说，达到手写nginx配置文件，才是合格的。
```

## 通过官网yum仓库默认安装的nginx.conf

```
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
~       
```

## docker的安装

## docker常用命令

### 外部文件拷入docker容器中

```shell
docker cp 文件路径 容器名称:路径
```

例如,将打包好的sql文件拷入容器根目录下

```shell
docker lse.sql mtsql-test:/
```

### 查看容器的ip地址

```shell
docker inspect 容器id  | grep IPAddress
```

### 检测redis是否连接成功代码

```java
import java.io.*;
import java.net.Socket;

public class redis {
    public static void main(String[] args) throws IOException {
        // 连接 Redis 服务器
        Socket socket = new Socket("localhost", 6379);

        // 创建输入输出流
        InputStream input = socket.getInputStream();
        OutputStream output = socket.getOutputStream();

        // 发送Redis命令
        String setCommand = "*3\r\n$3\r\nSET\r\n$3\r\nkey\r\n$5\r\nvalue\r\n";
        output.write(setCommand.getBytes());

        // 读取Redis服务器的响应
        byte[] buffer = new byte[1024];
        int bytesRead = input.read(buffer);
        String response = new String(buffer, 0, bytesRead);
        System.out.println(response);

        // 关闭连接
        socket.close();
    }
}

```

如果成功将返回+OK

## docker安装nginx

```shell
docker pull nginx
```

拉取镜像

```shell
docker images
```

查看是否拉取成功

### 创建挂载目录

```shell
mkdir -p /home/nginx/conf

mkdir -p/home/nginx/log

mkdir -p/home/nginx/html
```

### 生成容器

```shell
docker run --name nginx -p 9001:80 -d nginx
```

本机端口式9001，可以通过\_**ip:9001**\_来访问，但并不绝对是比如我的虚拟机就是需要通过

```shell
docker ps
```

查看我的是\_**0.0.0.0:9001**\_，才能运行

### 文件复制到宿主机

```shell
docker cp nginx:/etc/nginx/nginx.conf /home/nginx/conf/nginx.conf

docker cp nginx:/etc/nginx/conf.d /home/nginx/conf/conf.d

docker cp nginx:/usr/share/nginx/html /home/nginx/
```

### 关闭

```shell
docker stop nginx
```

### 删除

```shell
docker rm nginx
```

### 重启

```shell
docker run -p 9002:80 --name nginx -v /home/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v /home/nginx/conf/conf.d:/etc/nginx/conf.d -v /home/nginx/log:/var/log/nginx -v /home/nginx/html:/usr/share/nginx/html -d nginx:latest
```

通过复制出来的配置文件运行，就可以改外面的配置文件

## docker安装mysql

```shell
docker pull mysql:latest

docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql


```

## docker安装redis

```shell
docker pull redis

mkdir /home/redis/conf
mkdir /home/redis/data

cd /home/redis/conf
touch redis.conf

vi redis.conf
或者是
vim redis.conf
```

去官网上拷贝redis.conf

```
千万别忘了注释下面的语句
bind 0.0.0.0
！！！！！！！！!上面这行一定要注释掉



protected-mode no

#注意修改这里端口，根据你实际暴露端口情况配置
port 6380

#注意这里要把后台运行设置为no，避免docker后台运行冲突
daemonize no

#注意修改这里的目录为容器内目录，默认reids进来是在/data/目录
dir /data/

#注意修改这里的配置，yes开启持久化，no关闭持久化
appendonly yes
```

```shell
docker run --restart=always -p 6379:6379 --name redis --privileged=true -v /home/redis/conf/redis.conf:/etc/redis/redis.conf -v /home/redis/data:/data -d redis

```

启动后若是还是连接不上可以多试几次
