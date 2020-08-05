# MySQL on Windows

[最新版本](https://dev.mysql.com/downloads/mysql/)

[历史版本](https://downloads.mysql.com/archives/community/)

## MySQL 5.6

### 安装

[Installing MySQL5.6 on Microsoft Windows](https://dev.mysql.com/doc/refman/5.6/en/windows-install-archive.html)

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

### 卸载

- 卸载服务 **以管理员身份打开CMD**

```shell script
C:\> net stop MySQL56
C:\> mysqld --remove MySQL56
```

## MySQL 5.7

[Installing MySQL5.7 on Microsoft Windows](https://dev.mysql.com/doc/refman/5.7/en/windows-install-archive.html)

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
C:\> net stop MySQL57
C:\> mysqld --remove MySQL57
```
