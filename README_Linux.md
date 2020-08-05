# MySQL on CentOS

[最新版本](https://dev.mysql.com/downloads/mysql/)

[历史版本](https://downloads.mysql.com/archives/community/)

## MySQL 5.6

### 安装

[Installing MySQL5.6 on Unix/Linux](https://dev.mysql.com/doc/refman/5.6/en/binary-installation.html)

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

## MySQL 5.7

### 安装

[Installing MySQL5.7 on Unix/Linux](https://dev.mysql.com/doc/refman/5.7/en/binary-installation.html)

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
