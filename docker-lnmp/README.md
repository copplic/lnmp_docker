
#### 安装内容：

* nginx 1.9.2
* mysql 5.7
* php 7.4
* compose 2.0

#### 目录结构
```
docker-lnmp
├── docker-compose.yml 
├── nginx
│  ├── conf # nginx相关配置
│  ├── log  # nginx日志，访问日志、错误日志
│  └── ssl  # ssl证书
├── html # web文件目录
├── mysql
│  ├── conf # mysql相关配置
│  ├── log  # mysql日志
│  ├── init # 初始文件
│  └── data # mysql数据
├── php
│  ├── conf  # php相关配置
│  └── Dockerfile  # php镜像文件
```

### 安装


```shell
$ git clone ...
$ cd docker-lnmp
$ docker-compose up -d
Creating docker-lnmp_mysql_1 ... done
Creating docker-lnmp_php_1   ... done
Creating docker-lnmp_nginx_1 ... done
```

测试是否启动成功：

```shell
$ docker ps
a7c797cb350d        nginx:1.9.1        "/docker-entrypoint.…"   40 seconds ago      Up 38 seconds       0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   docker-lnmp_nginx_1
fcabcbdd2fbd        php:7.4-fpm    "docker-php-entrypoi…"   42 seconds ago      Up 40 seconds       0.0.0.0:9000->9000/tcp                     docker-lnmp_php_1
66857b56b61a        mysql:5.7           "docker-entrypoint.s…"   42 seconds ago      Up 40 seconds       0.0.0.0:3306->3306/tcp, 33060/tcp          docker-lnmp_mysql_1
```

此时，表示docker启动成功。

> 注：mysql默认用户名 `root`的密码为 `root`，同时添加用户名 `user`，密码为 `user123456`。

`docker-compose` 常用命令可参考 [https://yeasy.gitbook.io/docker_practice/compose/commands](https://yeasy.gitbook.io/docker_practice/compose/commands)

### 测试

* 测试是否可以正常连接 `nginx` 容器：

```shell
$ curl 127.0.0.1
this is index.html.
```

* 测试 `php` 文件是否可以正常执行：在浏览器中输入 `ip/p.php`，如果可正常显示phpinfo页面，则表面 `php` 文件可正常执行。
* 测试 `php` 是否可以正常连接 `mysql`：在浏览器中输入 `ip/db.php`，如果显示连接成功，则 `php` 可以正常连接 `mysql`。

### Laravel 开发

可以使用如下命令创建 `Laravel` 项目：

### 参考 资料
* [PHP Docker Official Images](https://hub.docker.com/_/php?tab=description)
