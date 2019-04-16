# JavaDock

参照 [Laradock](https://github.com/laradock/laradock) 写了个 JavaWeb 项目的运行容器。

不包括 data 数据和 log 日志。

## 一、使用步骤

1、复制env文件

```
cp env-example .env
```

2、修改 env 配置

3、部署 war 包到 www 目录

4、添加数据库初始化文件 create.sql 到 mysql/docker-entrypoint-initdb.d 目录下

- 从工具如 navicat 或 mysqldump 获取数据库sql文件，改名为 create.sql 放入上述指定目录
- 参考 createdb.sql.example，根据 .env 中配置的数据库名称和用户名称，在 create.sql 文件开头添加
```
CREATE DATABASE IF NOT EXISTS `数据库名` ;
GRANT ALL ON `数据库名`.* TO '用户名'@'%' ;
```


5、根据需要启动指定容器

```
docker-compose up -d
docker-compose up -d mysql redis tomcat
```

6、若修改了容器配置，直接重建镜像

```
docker-compose build <image_name>
```

7、重启容器

```
docker-compose restart <container_name>
```

8、查看指定容器的日志
```
docker-compose logs <container_name>
```
9、关闭指定容器
```
docker-compose stop <container_name>
```

10、关闭并删除容器
```
docker-compose down
```

## 二、注意事项

1、如果 war 包项目的启动会读取 mysql 表进行初始化，请务必添加 create.sql 文件进行数据库和表的初始化创建。

2、mysql 容器启动后，会根据 create.sql 文件在 .javadock/data/mysql 下生成数据文件，只要该目录下文件存在，再次创建或启动容器，不会再读取 create.sql 文件，即只会进行一次数据库初始化操作。

3、如 docker-compose up 时遇见意外错误，可尝试重启 docker。

4、项目使用镜像均为基础镜像，若项目存在特殊需求，请自行修改 Dockerfile。

5、有时 sql 建表过久，会导致依赖于 mysql 的 war 包项目启动失败，请待 mysql 初始化完成后再次启动 tomcat。
