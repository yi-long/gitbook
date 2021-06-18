[Reset Mysql Root password on Centos - Spiceworks](https://community.spiceworks.com/how_to/145495-reset-mysql-root-password-on-centos)

## Step 1: Stop Mysql

```shell
systemctl stop mysqld
```

## Step 2: set mysql env options

```shell
systemctl set-environment MYSQLD_OPTS=--skip-grant-tables
```

## Step 3: Start Mysql

```shell
systemctl start mysqld
```

## Step 4: Update Password using query

```mysql
mysql> UPDATE mysql.user SET authentication_string = PASSWORD ('ENTER_NEW_PASSWORD') WHERE User = 'root' AND Host = 'localhost';
mysql> FLUSH PRIVILEGES;
mysql> quit
```

## Step 5: Stop Mysql

```shell
systemctl stop mysqld
```

## Step 6: Unset enviroment

```shell
systemctl unset-environment MYSQLD_OPTS
```

## Step 7: Star mysql normal

```shell
systemctl start mysqld
```

