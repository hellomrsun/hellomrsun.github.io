---
layout: post
title: How to backup and restore database in SQL Server
description: How to backup and restore database in SQL Server
excerpt_separator:  <!--more-->
tags: SQL
canonical_url: 'https://sunjiangong.com/how-to-backup-and-restore-database-in-sql-server/'
---


If you want to backup and restore one database in SQL Server.


### 1. Create a shared folder, and add everyone with read/write right.

<br/>

### 2. Backup your database.

You can use the following script :

```sql
backup database DatabaseName to disk ='\\SharedFolder\backup_database\DatabaseBackup.bak' with INIT, stats=10
```

<br/>

<!--more-->

### 3. Restore your database

You have two methods to restore the database.

- **Use command line**

If your database exists, you can drop it.

```sql
DROP DATABASE DatabaseName
```

Recreate it:

```sql
CREATE DATABASE DatabaseName
```

Find the logical names for the data files and log files of the database backup.

```sql
restore filelistonly from disk='\\SharedFolder\backup_database\DatabaseBackup.bak'
```

Then you can restore your database with the following information.
 
```sql
RESTORE DATABASE DFM_INT_FI
  FROM DISK = '\\SharedFolder\backup_database\DataBaseBackup.bak'
  WITH REPLACE,
  MOVE 'DB_PRIMARY1' TO 'c:\temp\DB.mdf',
  MOVE 'DB_PRIMARY2' TO 'c:\temp\DB2ndf',
  MOVE 'DB_log' TO 'c:\temp\DB_log.ldf';
```

 
- **Use SSMS**

Right Click DataBases, and then click "Restore database..."

![](./../../../assets/images/BackupAndRestoreSqlServer/01_restore.png)


Choose "Device", and then add the backup file

![](./../../../assets/images/BackupAndRestoreSqlServer/02_restore_devise.png)
 

And then click OK, SSMS will restore the database itself.

 
![](./../../../assets/images/BackupAndRestoreSqlServer/03_restore.png)


 