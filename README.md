# JavaDock

参照 [Laradock](https://github.com/laradock/laradock) 写了个 JavaWeb 项目的运行容器。

不包括 data 数据和 log 日志。


1、复制env文件

```
cp env-example .env
```

2、修改 env 配置

3、根据需要启动指定容器

```
docker-compose up -d
docker-compose up -d mysql redis tomcat
```

4、如果修改了容器配置，直接重建镜像

```
docker-compose build <image_name>
```

5、重启容器

```
docker-compose restart <container_name>
```
