---
layout: post
# title: SQL server full-text index and its stop words
# description: SQL server full-text index and its stop words
# excerpt_separator:  <!--more-->
# tags: SQL-Server
# canonical_url: 'https://sunjiangong.com/sql-server-full-text-index-stop-words-stop-list/'
read_time: true
show_date: true
title:  MS SQL server full-text index and its stop words
date:   2021-06-12 08:00:00 +0100
description: MS SQL server full-text index and its stop words, fulltext index, Microsoft
img: posts/20210612-Fulltext-stoplist/3-fulltext-index-architecture.gif
tags: [SQLServer, FullText, Index]
author: SUN Jiangong
# github:  hellomrsun
mathjax: yes
---

Full-text index is different from clustered and non-clustered index in SQL Server.

# Clustered and non-clustered index use a B-tree structure.

One table can have only one clustered index. And table data is physically ordered and stored into pages based on the clustered index. Page is the fundamental unit of data storage in SQL Server.

The table data is organized with root node (type: INDEX_PAGE), intermediate nodes (type: INDEX_PAGE) and leaf nodes (type: DATA_PAGE).

<br/>

## Clustered index structure:

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/1-clustered-index-structure.jpg)

<!--more-->

Non-clustered index's leaf nodes are INDEX_PAGEs, 
instead of DATA_PAGEs, as table data can only be physcially ordered by clustered index. Non-clustered index's leaf nodes point to the clustered index's leaf nodes (DATA_PAGE).

<br/>

## Clustered index vs non-clustered index:

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/2-clustered-index-vs-non-clustered-index.PNG)

<br/>

**Full-text index is an inverted, stacked, compressed index structure.**

It's based on individual **tokens** from the text being indexed, built and maintained by the Full-Text Engine of SQL Server. The size of a full-text index is limited only by the available memory resources of the computer on which the instance of SQL Server is running.

<br/>

# Full-text search architecture:

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/3-fulltext-index-architecture.gif)

The full-text gatherer works with the full-text crawl threads. It is responsible for scheduling and driving the population of full-text indexes, and also for monitoring full-text catalogs.

When a full-text population (also known as a crawl) is initiated, the Full-Text Engine pushes large batches of data into memory and notifies the filter daemon host. 

The host filters and word breaks the data and converts the converted data into inverted word lists. 

The full-text search then pulls the converted data from the word lists, processes the data to remove stopwords, and persists the word lists for a batch into one or more inverted indexes.

Inverted index flow:

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/9-inverted-index.jpg)

<br/>

## Full-text index creation:


### Create a working table

Let's firstly create a client table.

```sql
CREATE TABLE dbo.Client (
    ClientId		INT IDENTITY(1,1) NOT NULL,
    FirstName		VARCHAR(50) NOT NULL, 
    LastName		VARCHAR(50) NOT NULL,
    EmailAddress	VARCHAR(50) NOT NULL,
    CreationDate	DATETIME NOT NULL
    CONSTRAINT [PK_Client] PRIMARY KEY CLUSTERED ([ClientId] ASC)
)
```
<br/>

### Insert fake data:

You can generate fake data with mockaroo.com, and then insert them into the table.

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/10-mockaroo.PNG)

Then, create more fake data with **CROSS JOIN**.

```sql
INSERT INTO dbo.Client (FirstName, LastName, EmailAddress, CreationDate)
SELECT TOP 100000 c1.[FirstName], c2.[LastName], REPLACE(NEWID(),'-','') + '@gmail.com',
DATEADD(HOUR,CAST(RAND(CHECKSUM(NEWID())) * 19999 as INT) + 1 ,'2006-01-01')
FROM [dbo].Client c1
CROSS JOIN Client c2

GO 50000 --repeat 50000 times
```


### Create full-text catelog 

A full-text catalog is a logical concept that refers to a group of full-text indexes. Catalogs makes it easier for maintaining full text indexes.

- SQL Server 2005: A full-text catalog is a physical structure that must reside on the local hard drive associated with the SQL Server instance. Each catalog is part of a specific filegroup. If no filegroup is specified when the catalog is created, the default filegroup is used.
- SQL Server 2008: A full-text catalog is a logical concept that refers to a group of full-text indexes. The catalog is not associated with a filegroup.

```sql
CREATE FULLTEXT CATALOG [FT_CATALOG_Client] WITH ACCENT_SENSITIVITY = OFF
```

<br/>

### Create full-text index:

```sql
CREATE FULLTEXT INDEX ON dbo.Client(
	[FirstName] language 1033,
	[LastName] language 1033 -- LCID(Local Identifier) for US English
)
KEY INDEX [PK_Client] ON ([FT_CATALOG_Client], FILEGROUP [PRIMARY])
WITH CHANGE_TRACKING AUTO;
```

Search for clients with LastName "Petrie" using **CONTAINS** with full-text index:

```sql
SELECT TOP 1 * FROM dbo.Client WHERE CONTAINS(LastName, 'Petrie')
```

You can see it's working fine.

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/4-fulltext-search-contains.PNG)

<br/>

But you won't find the user with LastName "a" with full-text index.

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/5-fulltext-search-contains-stopword.PNG)

This is because "a" is a stopword by default in US English in SQL Server.

You can right-click the table "dbo.Client", then choose "Full-text index", then choose "Properties" to check the stoplist options. You can see the it use "System" stoplist.

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/6-fulltext-search-stoplist-option.PNG)

You also can see the full-text index's columns are using "English".

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/7-fulltext-search-stoplist-option-language.PNG)

<br/>

You can check the stopwords on US English in SQL Server with its language_id with the following SQL.

```sql
select * from sys.fulltext_system_stopwords where language_id = 1033
```

<br/>
There are 154 words in the result list:

$,0,1,2,3,4,5,6,7,8,9,
A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z,
about,after,all,also,an,and,another,any,are,as,at,be,
because,been,before,being,between,both,but,by,came,can,
come,could,did,do,does,each,else,for,from,get,got,had,
has,have,he,her,here,him,himself,his,how,if,in,into,
is,it,its,just,like,make,many,me,might,more,most,much,
must,my,never,no,now,of,on,only,or,other,our,out,over,
re,said,same,see,should,since,so,some,still,such,take,
than,that,the,their,them,then,there,these,they,this,
those,through,to,too,under,up,use,very,want,was,way,
we,well,were,what,when,where,which,while,who,will,with,
would,you,your.

<br/>

So if we disable the default System stopwords, the full-text search will work.

We can disable the stoplist in the index creation.

```sql
CREATE FULLTEXT INDEX ON dbo.Client(
	[FirstName] language 1033,
	[LastName]  language 1033 -- LCID(Local Identifier) for US English
)
KEY INDEX [PK_Client] ON ([FT_CATALOG_Client], FILEGROUP [PRIMARY])
WITH STOPLIST = OFF, CHANGE_TRACKING AUTO;
```

Then the search will work.

![](./../../../assets/img/posts/20210612-Fulltext-stoplist/8-fulltext-search-stoplist-disabled.PNG)


<br/>
<br/>

**References:**
- https://sqlhints.com/tag/clustered-index-b-tree-structure/
- https://www.mssqltips.com/sqlservertutorial/9133/sql-server-nonclustered-indexes/
- https://docs.microsoft.com/en-us/sql/relational-databases/search/full-text-search?view=sql-server-ver15
- https://community.hitachivantara.com/s/article/search-the-inverted-index