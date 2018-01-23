---
layout: post
title: Useful Postgres Commands
tags:
- postgres
- pg
- commands
---

### Login

```
psql -U username postgres
```

### Show a list of Tables

```
\dt
```

### Lists

#### Databases

```
\list
```

#### Users

```
\du
```

### Quit

```
\q
```

### Changing Owner and Privileges

The issues I came accross when trying to grant privileges/create a new database included that I had to be logged in as the owner of the databse and that I did not have permissions. The errors included:

* `peer authentication failed for user "username"
* `must be owner of database db_name
* `permission denied to drop role`

You may be asked for a password, e.g. the deploy user's password. If you log on using access keys, you may need to (re)set this:

```
sudo su
sudo passwd deploy
```

Log in as the user that owns the database, e.g. postgres (after `exit` to get back to the deploy account):

```
sudo -u postgres psql db_name postgres _db_name postgres
```

To change the database owner: `ALTER DATABASE db_name OWNER TO username;`

To grant privileges: `GRANT ALL PRIVILEGES ON DATABSE database TO username;`