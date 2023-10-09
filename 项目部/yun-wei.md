# 运维

## 1.1 docker的安装

## 1.2 docker常用命令

### 1.2.1外部文件拷入docker容器中

```shell
docker cp 文件路径 容器名称:路径
```

例如,将打包好的sql文件拷入容器根目录下

```shell
docker lse.sql mtsql-test:/
```

### 1.2.2 查看容器的ip地址

```shell
docker inspect 容器id  | grep IPAddress
```

### 1.2.3 检测redis是否连接成功代码

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

## 1.3 docker安装nginx

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

本机端口式9001，可以通过_**ip:9001**_来访问，但并不绝对是比如我的虚拟机就是需要通过

```shell
docker ps
```

查看我的是_**0.0.0.0:9001**_，才能运行

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

## 1.4 docker安装mysql

```shell
docker pull mysql:latest

docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql


```

## 1.5 docker安装redis

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
