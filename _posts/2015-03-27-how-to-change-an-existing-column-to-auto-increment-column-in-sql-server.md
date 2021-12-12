---
layout: post
read_time: true
show_date: true
title:  How to change an existing column to auto-increment column in SQL Server?
date:   2015-03-27 08:00:00 +0100
description: How to change an existing column to auto-increment column in SQL Server?
img: posts/uncategorized/sqlserver.PNG
tags: [SQLServer]
author: SUN Jiangong
mathjax: yes
---


In SQL server when you want to make an existing column to be auto-incremented.

The following code is not working:

```sql
ALTER TABLE [dwh].[ExchangeRate]
ALTER COLUMN [ExchangeRateId] Int Identity(1, 1)
```

What you could do is :
- Create a new column with auto-increment
- Delete existing column constraint
- Delete the existing column
- Rename the new column back
- Add deleted constraint

<br/>

#### Step 1: Create a new column

```sql
ALTER TABLE [dwh].[ExchangeRate]
ADD [ExchangeRateId2] Int Identity(1, 1)
```

#### Step 2: Delete existing constraint

```sql
ALTER TABLE [dwh].[ExchangeRate]
DROP CONSTRAINT [IxExchangeRate_ExchangeRateId_U_NC_]
```

#### Step 3: Delete existing column

```sql
ALTER TABLE [dwh].[ExchangeRate]
DROP COLUMN [ExchangeRateId]
```

#### Step 4: Rename new column

```sql
Exec sp_rename 'dwh.ExchangeRate.ExchangeRateId2', 'ExchangeRateId','COLUMN'
```

#### Step 5: Add deleted contraint

```sql
ALTER TABLE [dwh].[ExchangeRate] ADD  CONSTRAINT [IxExchangeRate_ExchangeRateId_U_NC_] PRIMARY KEY CLUSTERED 
(
[ExchangeRateId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, IGNORE_DUP_KEY = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, FILLFACTOR = 90) ON [PRIMARY]
```

