# docker 





# Mysql



包含具体参数配置

https://ost.51cto.com/posts/24358

```bash
docker run -p 3306:3306 --name mysql -itd \
 # 将主机的 /Users/bytedance/Desktop/whig/docker/amd64_mysql/log 目录挂载到容器的 /var/log/mysql 目录，用于存储 MySQL 的日志文件。
 -v /Users/bytedance/Desktop/whig/docker/amd64_mysql/log:/var/log/mysql \
 # 将主机的 /Users/bytedance/Desktop/whig/docker/amd64_mysql/data 目录挂载到容器的 /var/lib/mysql 目录，用于存储 MySQL 的数据文件。
 -v /Users/bytedance/Desktop/whig/docker/amd64_mysql/data:/var/lib/mysql \
 # 将主机的 /Users/bytedance/Desktop/whig/docker/amd64_mysql/conf 目录挂载到容器的 /etc/mysql 目录，用于存储 MySQL 的配置文件。
 #就是不要写这句话被 如何映射conf位置将会报错呗
 -v /Users/bytedance/Desktop/whig/docker/amd64_mysql/conf:/etc/mysql \
 # 将主机的 /home/mysql/mysql-files 目录挂载到容器的 /var/lib/mysql-files 目录，用于存储 MySQL 的文件数据。
 -v /Users/bytedance/Desktop/whig/docker/amd64_mysql/mysql-files:/var/lib/mysql-files \
 # 设置 MySQL 的 root 用户密码为 root。这个参数使用了环境变量来传递密码信息。
 -e MYSOL_ROOT_PASSWORD=1234567 \
 # 以后台模式运行 MySQL 容器，并使用 mysql:5.7.42-oracle 镜像作为容器镜像。
 -d amd64/mysql:latest \
 # 设置 MySQL 的字符集为 utf8mb4，并使用 utf8mb4_unicode_ci 排序规则。这个参数可以确保 MySQL 能够正确地处理 Unicode 字符。
 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
 # ---命令结束，下面都是输出
 # 输出的是容器的 ID，表示容器已成功启动。
```





# redis



# kafka

