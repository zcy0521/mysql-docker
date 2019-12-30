# MySQL

[最新版本](https://dev.mysql.com/downloads/mysql/)

[历史版本](https://downloads.mysql.com/archives/community/)

## Windows host

- MySQL 5.5

[https://dev.mysql.com/doc/refman/5.5/en/windows-install-archive.html](https://dev.mysql.com/doc/refman/5.5/en/windows-install-archive.html)

```shell script
# 编辑 my.ini
[client]
port=3306
[mysql]
default-character-set=utf8
[mysqld]
port=3306
basedir="C:/Program Files/MySQL/MySQL Server 5.5"
datadir="$PWD/data"
character-set-server=utf8
default-storage-engine=INNODB

# 安装服务 **以管理员身份打开CMD**
C:\> "C:\Program Files\MySQL\MySQL Server 5.5\bin\mysqld" --install MySQL55 --defaults-file="C:\Program Files\MySQL\MySQL Server 5.5\my.ini"
C:\> net start MySQL55

# root登录 **密码为空**
C:\> "C:\Program Files\MySQL\MySQL Server 5.5\bin\mysql" -u root -p
```

- MySQL 5.6 安装

[https://dev.mysql.com/doc/refman/5.6/en/windows-install-archive.html](https://dev.mysql.com/doc/refman/5.6/en/windows-install-archive.html)

```shell script
# 编辑 my.ini
[client]
port=3306
[mysql]
default-character-set=utf8
[mysqld]
port=3306
basedir="C:/Program Files/MySQL/MySQL Server 5.6"
datadir="$PWD/data"
character-set-server=utf8
default-storage-engine=INNODB

# 安装服务 **以管理员身份打开CMD**
C:\> "C:\Program Files\MySQL\MySQL Server 5.6\bin\mysqld" --install MySQL56 --defaults-file="C:\Program Files\MySQL\MySQL Server 5.6\my.ini"
C:\> net start MySQL56

# root登录 **密码为空**
C:\> "C:\Program Files\MySQL\MySQL Server 5.6\bin\mysql" -u root -p
```

- MySQL 5.7  安装

[https://dev.mysql.com/doc/refman/5.7/en/windows-install-archive.html](https://dev.mysql.com/doc/refman/5.7/en/windows-install-archive.html)

```shell script
# 编辑 my.ini **5.7.18版本开始不再提供 `my-default.ini` 需要新建**
[client]
port=3306
[mysql]
default-character-set=utf8
[mysqld]
port=3306
basedir="C:/Program Files/MySQL/MySQL Server 5.7"
datadir="$PWD/data"
character-set-server=utf8
default-storage-engine=INNODB

# 初始化data目录 **5.7.7版本开始默认不包含 `/data` 安装服务前需要初始化**
C:\> "C:\Program Files\MySQL\MySQL Server 5.7\bin\mysqld" --initialize-insecure

# 安装服务 **以管理员身份打开CMD**
C:\> "C:\Program Files\MySQL\MySQL Server 5.7\bin\mysqld" --install MySQL57 --defaults-file="C:\Program Files\MySQL\MySQL Server 5.7\my.ini"
C:\> net start MySQL57

# root登录 **密码为空**
C:\> "C:\Program Files\MySQL\MySQL Server 5.7\bin\mysql" -u root -p
```

> [5.7.18版本开始不再提供 `my-default.ini` 需要新建](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html)

> [5.7.7版本开始默认不包含 `/data` 安装服务前需要初始化](https://dev.mysql.com/doc/refman/5.7/en/windows-initialize-data-directory.html)

> --initialize 为root用户生成随机密码 --initialize-insecure 为root用户生成空密码

- 卸载

```shell script
# 卸载服务 **以管理员身份打开CMD**
C:\> net stop MySQL5X
C:\> mysqld --remove MySQL5X
```

## Linux host

- MySQL 5.5

[https://dev.mysql.com/doc/refman/5.5/en/binary-installation.html](https://dev.mysql.com/doc/refman/5.5/en/binary-installation.html)

```shell script
# 卸载 `mariadb`
$ yum list installed | grep mariadb
$ yum -y remove mariadb-libs-xxx

# 安装依赖
$ yum install libaio

# 添加mysql组和mysql用户
$ groupadd mysql
$ useradd -r -g mysql -s /bin/false mysql

# 将tar解压并复制到/usr/local目录
$ tar zxvf mysql-5.5.58-linux-glibc2.12-x86_64.tar.gz
$ cp -r mysql-5.5.58-linux-glibc2.12-x86_64 /usr/local/mysql

# 将 `my.cnf` 复制到 `/etc` 目录中
$ cd /usr/local/mysql
$ cp support-files/my-medium.cnf /etc/my.cnf

# 初始化数据目录
$ cd /usr/local/mysql
$ chown -R mysql .
$ chgrp -R mysql .
$ scripts/mysql_install_db --user=mysql \
  --basedir=/usr/local/mysql \
  --datadir=/usr/local/mysql/data
$ chown -R root .
$ chown -R mysql data

# 启动服务
$ cd /usr/local/mysql
$ bin/mysqld_safe --user=mysql &

# 开机自动运行
$ cd /usr/local/mysql
$ cp support-files/mysql.server /etc/init.d/mysql.server

# root登录 **密码为空**
$ cd /usr/local/mysql
$ bin/mysql -u root -p
```

- MySQL 5.6

[https://dev.mysql.com/doc/refman/5.6/en/binary-installation.html](https://dev.mysql.com/doc/refman/5.6/en/binary-installation.html)

```shell script
# 卸载 `mariadb`
$ yum list installed | grep mariadb
$ yum -y remove mariadb-libs-xxx

# 安装依赖
$ yum install libaio
$ yum install perl perl-Data-Dumper

# 添加mysql组和mysql用户
$ groupadd mysql
$ useradd -r -g mysql -s /bin/false mysql

# 将tar解压并复制到/usr/local目录
$ tar zxvf mysql-5.6.38-linux-glibc2.12-x86_64.tar.gz
$ cp -r mysql-5.6.38-linux-glibc2.12-x86_64 /usr/local/mysql

# 初始化数据目录
$ cd /usr/local/mysql
$ scripts/mysql_install_db --user=mysql \
  --basedir=/usr/local/mysql \
  --datadir=/usr/local/mysql/data

# 启动服务
$ cd /usr/local/mysql
$ bin/mysqld_safe --user=mysql &

# 开机自动运行
$ cd /usr/local/mysql
$ cp support-files/mysql.server /etc/init.d/mysql.server

# root登录 **密码为空**
$ cd /usr/local/mysql
$ bin/mysql -u root -p
```

> 不用将 `my.cnf` 复制到 `/etc` 目录中，在初始化数据目录时，会在/mysql目录中生成my.cnf

- MySQL 5.7 安装

[https://dev.mysql.com/doc/refman/5.7/en/binary-installation.html](https://dev.mysql.com/doc/refman/5.7/en/binary-installation.html)

```shell script
# 卸载 `mariadb`
$ yum list installed | grep mariadb
$ yum -y remove mariadb-libs-xxx

# 安装依赖
$ yum install libaio

# 添加mysql组和mysql用户
$ groupadd mysql
$ useradd -r -g mysql -s /bin/false mysql

# 将tar解压并复制到/usr/local目录
$ tar zxvf mysql-5.7.21-linux-glibc2.12-x86_64.tar.gz
$ cp -r mysql-5.7.21-linux-glibc2.12-x86_64 /usr/local/mysql

# 初始化数据目录
$ cd /usr/local/mysql
$ mkdir mysql-files
$ chown mysql:mysql mysql-files
$ chmod 750 mysql-files
$ bin/mysqld --initialize --user=mysql \
  --basedir=/usr/local/mysql \
  --datadir=/usr/local/mysql/data
$ bin/mysql_ssl_rsa_setup

# 启动服务
$ cd /usr/local/mysql
$ bin/mysqld_safe --user=mysql &

# 开机自动运行
$ cd /usr/local/mysql
$ cp support-files/mysql.server /etc/init.d/mysql.server

# root登录 **密码为安装时生成的随机密码**
$ cd /usr/local/mysql
$ bin/mysql -u root -p
```

> 不用将 `my.cnf` 复制到 `/etc` 目录中，在初始化数据目录时，会在/mysql目录中生成my.cnf

> 初始化数据目录时，日志会提示生成默认密码 `[Note] A temporary password is generated for root@localhost`

- MySQL 5.5卸载

```shell script
# 停止mysql服务
$ cd /usr/local/mysql
$ bin/mysqladmin -u root -p shutdown

# 删除mysql目录
$ whereis mysql
$ rm -r /usr/lib64/mysql
$ rm -r /usr/local/mysql

# 删除/etc/my.cnf
$ rm /etc/my.cnf

# 删除/etc/init.d/mysql.server
$ rm /etc/init.d/mysql.server
$ bin/mysqladmin -uroot -proot shutdown
```

- MySQL 5.6 5.7 卸载

```shell script
# 停止mysql服务
$ cd /usr/local/mysql
$ bin/mysqladmin -u root -p shutdown

# 删除mysql目录
$ whereis mysql
$ rm -r /usr/lib64/mysql
$ rm -r /usr/local/mysql

# 删除/etc/init.d/mysql.server
$ rm /etc/init.d/mysql.server
```

## Docker

[Docker Hub](https://hub.docker.com/r/mysql/mysql-server)

[MySQL Installation Guide](https://dev.mysql.com/doc/mysql-installation-excerpt/8.0/en/docker-mysql-getting-started.html)

### run

```shell script
$ sudo docker pull mysql/mysql-server

$ sudo docker run \
  -d \
  --name mysql \
  -p 3306:3306 \
  --mount type=bind,src=/mysql/my.cnf,dst=/etc/my.cnf \
  --mount type=bind,src=/mysql/datadir,dst=/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=root \
  -e MYSQL_ROOT_HOST=% \
  mysql/mysql-server
```

### docker-compose

- stack.yml

```yaml
version: '3.1'

services:
  mysql:
    image: mysql/mysql-server
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    hostname: mysql
    container_name: mysql
    ports:
      - 3306:3306
    volumes:
      - ${HOME}/appdata/mysql/datadir:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_ROOT_HOST=%

  adminer:
    image: adminer
    restart: always
    hostname: adminer
    container_name: adminer
    ports:
      - 13306:8080
```

- 运行

```shell script
$ sudo docker-compose -f stack.yml up -d
$ sudo docker exec -it mysql bash
```
