# MySQL

## Usage

- 运行 msql

```shell script
git clone https://github.com/zcy0521/mysql-docker.git
sudo docker pull mysql
sudo docker-compose up -d
```

- 配置 `mysql.cnf`

```shell script
vi conf.d/mysql.cnf
sudo docker restart mysql
```

## Docker

- [Get Docker Engine - Community for Debian](https://docs.docker.com/install/linux/docker-ce/debian/)

```shell script
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
```
  
- [Install Docker Compose](https://docs.docker.com/compose/install/)

```shell script
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

## MySQL Docker

- [Docker Hub](https://hub.docker.com/_/mysql)

```shell script
sudo docker pull mysql
sudo docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_ROOT_HOST=% -p 3306:3306 mysql
sudo docker exec -it mysql bash
sudo docker stop mysql
sudo docker rm mysql
```

## MySQL on Windows

[最新版本](https://dev.mysql.com/downloads/mysql/)

[历史版本](https://downloads.mysql.com/archives/community/)

### MySQL 5.6

https://dev.mysql.com/doc/refman/5.6/en/windows-install-archive.html

- 编辑 `my.ini`

```shell script
[client]
port=3306
[mysql]
default-character-set=utf8
[mysqld]
port=3306
basedir="C:/MySQL/MySQL Server 5.6"
datadir="$PWD/data"
character-set-server=utf8
default-storage-engine=INNODB
```

- 安装MySQL **以管理员身份打开CMD**

```shell script
C:\> "C:\Program Files\MySQL\MySQL Server 5.6\bin\mysqld" --install MySQL56 --defaults-file="C:\Program Files\MySQL\MySQL Server 5.6\my.ini"
C:\> net start MySQL56
```

- 登录

```shell script
C:\> "C:\Program Files\MySQL\MySQL Server 5.6\bin\mysql" -u root -p
密码为空
```

### MySQL 5.7

https://dev.mysql.com/doc/refman/5.7/en/windows-install-archive.html

- 编辑 `my.ini`

```shell script
[client]
port=3306
[mysql]
default-character-set=utf8
[mysqld]
port=3306
basedir="C:/MySQL/MySQL Server 5.7"
datadir="$PWD/data"
character-set-server=utf8
default-storage-engine=INNODB
```

> [5.7.18版本开始不再提供 `my-default.ini` 需要新建](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html)

- 初始化data目录

```shell script
C:\> "C:\Program Files\MySQL\MySQL Server 5.7\bin\mysqld" --initialize-insecure
```

> [5.7.7版本开始默认不包含 `/data` 安装服务前需要初始化](https://dev.mysql.com/doc/refman/5.7/en/windows-initialize-data-directory.html)

> --initialize 为root用户生成随机密码 --initialize-insecure 为root用户生成空密码

- 安装MySQL **以管理员身份打开CMD**

```shell script
C:\> "C:\Program Files\MySQL\MySQL Server 5.7\bin\mysqld" --install MySQL57 --defaults-file="C:\Program Files\MySQL\MySQL Server 5.7\my.ini"
C:\> net start MySQL57
```

- 登录

```shell script
C:\> "C:\Program Files\MySQL\MySQL Server 5.7\bin\mysql" -u root -p
密码为空
```

### 卸载

- 卸载服务 **以管理员身份打开CMD**

```shell script
C:\> net stop MySQL5X
C:\> mysqld --remove MySQL5X
```

## MySQL on CentOS

[最新版本](https://dev.mysql.com/downloads/mysql/)

[历史版本](https://downloads.mysql.com/archives/community/)

### MySQL 5.6

https://dev.mysql.com/doc/refman/5.6/en/binary-installation.html

- 卸载 `mariadb`

```shell script
yum list installed | grep mariadb
yum -y remove mariadb-libs-xxx
```

- 安装依赖

```shell script
yum install libaio
yum install perl perl-Data-Dumper
```

- 安装MySQL

```shell script
groupadd mysql
useradd -r -g mysql -s /bin/false mysql
wget https://cdn.mysql.com//Downloads/MySQL-5.6/mysql-5.6.48-linux-glibc2.12-x86_64.tar.gz
tar zxvf mysql-5.6.48-linux-glibc2.12-x86_64.tar.gz
cp -r mysql-5.6.48-linux-glibc2.12-x86_64 /usr/local/mysql
/usr/local/mysql/scripts/mysql_install_db --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
```

> 会在`/usr/local/mysql`目录中生成`my.cnf`

- 启动

```shell script
/usr/local/mysql/bin/mysqld_safe --user=mysql &
/usr/local/mysql/bin/mysql -u root -p
密码为空
```

- 服务

```shell script
cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql.server
sudo service mysql enable
sudo service mysql start
```

### MySQL 5.7

https://dev.mysql.com/doc/refman/5.7/en/binary-installation.html

- 卸载 `mariadb`

```shell script
yum list installed | grep mariadb
yum -y remove mariadb-libs-xxx
```

- 安装依赖

```shell script
yum install libaio
```

- 安装MySQL

```shell script
groupadd mysql
useradd -r -g mysql -s /bin/false mysql
wget https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.30-linux-glibc2.12-x86_64.tar.gz
tar zxvf mysql-5.7.30-linux-glibc2.12-x86_64.tar.gz
cp -r mysql-5.7.30-linux-glibc2.12-x86_64 /usr/local/mysql
mkdir /usr/local/mysql/mysql-files
chown mysql:mysql /usr/local/mysql/mysql-files
chmod 750 /usr/local/mysql/mysql-files
/usr/local/mysql/bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
/usr/local/mysql/bin/mysql_ssl_rsa_setup
```

> 会在`/usr/local/mysql`目录中生成`my.cnf`

> 初始化数据目录时，日志会提示生成默认密码 `[Note] A temporary password is generated for root@localhost`

- 启动

```shell script
/usr/local/mysql/bin/mysqld_safe --user=mysql &
/usr/local/mysql/bin/mysql -u root -p
密码为空
```

- 服务

```shell script
cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql.server
sudo service mysql enable
sudo service mysql start
```

### 卸载

- 停止服务

```shell script
/usr/local/mysql/bin/mysqladmin -u root -p shutdown
```
- 删除mysql相关文件

```shell script
sudo rm -r /usr/lib64/mysql
sudo rm -r /usr/local/mysql
sudo rm /etc/init.d/mysql.server
```
