---
layout: post
tags:
- mysql
- cheatsheet
- development
---

## Copy a database from a remote server to a local computer

```
ssh user@server
cd platform/config/web/
mysqldump -u root cust_server_prodction > dump.sql
exit
scp user@server:platform/config/web/dump.sql ~/
mysql -u root cust_server_prodction < dump.sql
```

> To be prompted for the password use `mysqldump -u root -p db_name > dump.sql`

You may need to create the database locally before importing into it with the following

```
mysql -u root
create database cust_server_prodction;
show databases;
exit
```