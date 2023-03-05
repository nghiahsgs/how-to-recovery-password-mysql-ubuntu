# how-to-recovery-password-mysql-ubuntu
how to recovery password mysql ubuntu


## Step 1: Stop the MySQL server.

On Unix/Linux systems, you can do this by running the command 
```
sudo systemctl stop mysql.
```

## Step 2: Start the MySQL server with the --skip-grant-tables option.
Open the configuration file for MySQL, which is typically located at /etc/mysql/mysql.conf.d/mysqld.cnf on Unix/Linux systems.
<br/>
Find the [mysqld] section in the configuration file.
<br/>
Add the following line to the [mysqld] section:

```
skip-grant-tables
```
Save the configuration file.

Start the MySQL server.

On Unix/Linux systems, you can do this by running the command 
```
sudo systemctl start mysql.
```


Connect to the MySQL server as the root user with the command 
```
mysql -u root.
```
You won't be prompted for a password since you're connected as the root user.


## Step 3: Update password for 'root' user
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
