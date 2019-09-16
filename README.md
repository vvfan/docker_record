# docker_record

## 说明
本实例是根据自己在搭建PHP的docker环境中的总结

### docker-php
docker-php 是 根据 
php:7.2-fpm, nginx:alpine, mysql:5.7, redis:alpine
利用 docker-compose 编写的实例方法

#### 目录结构

```
app # 项目目录
	index.php
	test
		-test.php
data # 数据目录
	mysql
	redis

logs # 日志目录
	nginx
	mysql
	php-fpm

docker_self # docker目录
	docker-compose.yml
	mysql
		-Dockerfile
		-conf.d
			-my.conf
	nginx
		-Dockerfile
		-nginx.conf
		-conf.d
			-www.conf
	php
		-Dokcerfile
		-php-fpm.conf
		-php-fom.d
			-www.conf
		-idc.ini
	redis
		-Dockerfile
```



#### 启动与停止

>* 编写好完毕后，可使用 docker-compose up 启动
   有错误，则根据输出调试
>* 启动没问题后，以后可使用 docker-compose up -d 后台启动
   docker container ls 查看启动容器
   docker image ls 查看镜像列表
>* 停止服务,可使用 docker-compose stop

#### 缺点

>* 镜像太大
   FROM php:7.2-fpm
   非 alpine的镜像，默认是以 ubanutu 为基础的，
   可以使用 apt-get,docker-php-ext-*等命令
   但生成的镜像 非常大
   alpine镜像 只能 使用 apk 的方式安装软件包


## 待做
>* alpine镜像的制作
>* laradock的使用



