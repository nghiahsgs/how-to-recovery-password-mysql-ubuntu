# how-to-recovery-password-mysql-ubuntu
how to recovery password mysql ubuntu

## Step1: Open file config and add new lines
how to find mysql config file path
```
mysql --help | grep "Default options" -A 1
```

```
sudo vim /etc/mysql/my.cnf
```

```
[mysqld]

skip-grant-tables
```


## Step 2: Restart mysql
```
sudo service mysql restart
```

## Step 3: Login to mysql
```
mysql -u root
use mysql
select * from mysql.user where user = 'root';
```

## Step 4: Update password for 'root' user
```
UPDATE mysql.user set authentication_string = CONCAT('*', UPPER(SHA1(UNHEX(SHA1('mypass'))))) where user = 'root' and host = 'localhost';
FLUSH PRIVILEGES;
```

## Step 5: exit and remove new lines in file config
```
exit
sudo vim /etc/mysql/my.cnf
```

## Step 6: Restart mysql
```
sudo service mysql restart
```
