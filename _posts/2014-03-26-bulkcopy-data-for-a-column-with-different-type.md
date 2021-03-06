---
layout: post
title: BulkCopy data from source table to destination table with different column type in SQL Server
description: BulkCopy data from source table to destination table with different column type in SQL Server
excerpt_separator:  <!--more-->
tags: SQL-Server
canonical_url: 'https://sunjiangong.com/bulkcopy-data-from-source-table-to-destination-table-with-different-column-type-in-SQL-Server/'
---


I've encountered a problem when I do a sql bulk copy from a table in staging to the same table in production. 

The problem is that the same column has different types in the two tables.

<!--more-->

The error is the following when I bulkcopy the data:

```sql
The locale id '0' of the source column 'EntityId' and the locale id '1033' of thedestination column 'EntityId' do not match.
```

But this is not the source of the error.


After strugling several hours, a solution is to use a CONVERT when I synchronize the data.

```sql
SELECT Id, CONVERT(varchar(60), EntityId) as EntityId  FROM @TABLENAME WITH (NOLOCK) WHERE ID = @ID
```

Hope this helps! 

Enjoy coding!