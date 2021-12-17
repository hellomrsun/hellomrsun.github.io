---
layout: post
read_time: true
show_date: true
title:  BulkCopy data from source table to destination table with different column type in SQL Server
date:   2014-03-26 08:00:00 +0100
description: BulkCopy data from source table to destination table with different column type in SQL Server
img: posts/uncategorized/sqlserver.PNG
tags: [SQLServer]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/bulkcopy-data-from-source-table-to-destination-table-with-different-column-type-in-SQL-Server.html'
mathjax: yes
redirect_from:
  - /2014/03/26/bulkcopy-data-for-a-column-with-different-type.html
---


I've encountered a problem when I do a sql bulk copy from a table in staging to the same table in production. 

The problem is that the same column has different types in the two tables.

The error is the following when I bulkcopy the data:

```sql
The locale id '0' of the source column 'EntityId' and the locale id '1033' of thedestination column 'EntityId' do not match.
```

<!--more-->

But this is not the source of the error.


After strugling several hours, a solution is to use a CONVERT when I synchronize the data.

```sql
SELECT Id, CONVERT(varchar(60), EntityId) as EntityId  FROM @TABLENAME WITH (NOLOCK) WHERE ID = @ID
```

Hope this helps! 

Enjoy coding!