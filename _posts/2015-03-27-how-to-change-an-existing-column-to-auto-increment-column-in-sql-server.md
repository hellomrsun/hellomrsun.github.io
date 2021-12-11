---
layout: post
title: How to change an existing column to auto-increment column in SQL Server
description: How to change an existing column to auto-increment column in SQL Server, MS SQL Server
excerpt_separator:  <!--more-->
tags: SQL
canonical_url: 'https://sunjiangong.com/how-to-change-an-existing-column-to-auto-increment-column-in-sql-server/'
---


In SQL server when you want to make an existing column to be auto-incremented.

The following code is not working:

```sql
ALTER TABLE [dwh].[ExchangeRate]
ALTER COLUMN [ExchangeRateId] Int Identity(1, 1)
```

<!--more-->

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

