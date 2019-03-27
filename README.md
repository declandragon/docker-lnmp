## 简介
用 Docker 容器服务的方式搭建环境，易于维护、升级。使用前需了解 Docker 的基本概念，常用基本命令。
可以一条条命令执行docker命令来构建镜像，容器。这里推荐使用 docker-compose 来管理，执行项目，下面是使用流程。

相关软件版本：
- PHP 7.0/7.1/7.2
- MySQL 5.7
- Nginx 1.14
- Redis 4.0
- mongodb:4.0
- Rabbitmq:3-management

用到的 PHP 拓展(2019-03-27更新)：
- redis
- Swoole
- mongodb
- amqp 

## 使用
### 1.安装 Docker，Docker-compose  

### 2.docker-compose 构建项目
进入 docker-compose.yml 所在目录：
执行命令：
```
docker-compose build  #构建
docker-compose up     #启动
```  

如果没问题，下次启动时可以以守护模式启用，所有容器将后台运行：  
```
docker-compose up -d
``` 

可以这样查看日志
```
docker-compose logs -f
``` 

可以这样查看服务：
```
docker-compose ps
```

可以这样关闭容器并删除服务：
```
docker-compose down
```

### 3. 密码信息
    mongodb数据库信息：
        MONGODB_USERNAME: wl_user
        MONGODB_PASSWORD: rootroot
        MONGODB_DATABASE: declandragon  
 
	Mysql数据库信息：
        MYSQL_ROOT_PASSWORD: rootroot
        MYSQL_DATABASE: declandragon
        MYSQL_USER: declandragon
        MYSQL_PASSWORD: declandragon
		
	Redis信息：
        密码: zhangxuliang
		
	rabbitmq信息：
	    rabbitmq_VHOST：zxl_vhost  
        rabbitmq账号: minicart
	    rabbitmq密码：zhang