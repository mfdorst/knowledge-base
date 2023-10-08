# MySQL and MariaDB

## Log in to MySQL interpreter
If you are using socket authentication, mysql relies on your linux user authentication. This
requires you to run the command as root.
```
sudo mysql -u root
```
If you are using password authentication, you will need to supply the `-p` flag. This will cause
the interpreter to prompt you for your password.
```
mysql -u root -p
```

This also applies to `mysqldump`.

## Use a DB
```
> USE database;
```

## Create a DB dump
```
sudo mysqldump -u root db_name -r db_dump.sql
```
You may need to use the `-p` flag depending on your configuration.

## Load a DB dump
Create a new DB
```
sudo mysql -u root
> CREATE DATABASE new_db;
> exit
```
Load the DB dump
```
sudo mysql -u root new_db db_dump.sql
```
