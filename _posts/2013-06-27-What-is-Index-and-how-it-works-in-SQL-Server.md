---
layout: post
read_time: true
show_date: true
title:  What is Index and how it works in SQL Server?
date:   2013-06-27 08:00:00 +0100
description: What is Index and how it works in SQL Server?
img: posts/uncategorized/sqlserver.PNG
tags: [SqlServer]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/what-is-Index-and-how-it-works-in-SQL-Server.html'
---


### What is HEAP?

A heap is a table without a clustered index. One or more nonclustered indexes can be created on tables stored as a heap.

Data is stored in the heap without specifying an order. Usually data is initially stored in the order in which is the rows are inserted into the table, but the Database Engine can move data around in the heap to store the rows efficiently; so the data order cannot be predicted. 

To guarantee the order of rows returned from a heap, you must use the ORDER BY clause. 

To specify the order for storage of the rows, create a clustered index on the table, so that the table is not a heap.

<br />

### How heap works?

When we do a search in a heap, which is a table without clustered index, a full table scan will be performed. 

<!--more-->

### When use Heap?

When the table is very small.


### When not use Heap?

Do not use a heap when the data is frequently returned in a sorted order. A clustered index on the sorting column could avoid the sorting operation.

Do not use a heap when the data is frequently grouped together. Data must be sorted before it is grouped, and a clustered index on the sorting column could avoid the sorting operation.

Do not use a heap when ranges of data are frequently queried from the table. A clustered index on the range column will avoid sorting the entire heap.

Do not use a heap when there are no nonclustered indexes and the table is large. In a heap, all rows of the heap must be read to find any row.

### What is Index?

An index is an on-disk structure associated with a table or view that speeds retrieval of rows from the table or view. 

An index is made up of a set of pages (index nodes). 

An index contains keys built from one or more columns in the table or view. 

These keys are stored in a structure (B-tree) that enables SQL Server to find the row or rows associated with the key values quickly and efficiently.

You can create indexes on most columns in a table or a view. 

The exceptions are primarily those columns configured with large object (LOB) data types, such as image, text, and varchar(max).

### How it works?

If you search for a value in a indexed column, the query engine will start from Root node -> intermediate nodes -> leaf nodes. 

The leaf node will contain either the entire row of data or a pointer to that row, depending on whether the index is clustered or nonclustered.

### How index is used by query optimizer?

When this query is executed, the query optimizer evaluates each available method for retrieving the data and selects the most efficient method. The method may be a table scan, or may be scanning one or more indexes if they exist.


When performing a table scan, the query optimizer reads all the rows in the table, and extracts the rows that meet the criteria of the query. A table scan generates many disk I/O operations and can be resource intensive. However, a table scan could be the most efficient method if, for example, the result set of the query is a high percentage of rows from the table.


When the query optimizer uses an index, it searches the index key columns, finds the storage location of the rows needed by the query and extracts the matching rows from that location. Generally, searching the index is much faster than searching the table because unlike a table, an index frequently contains very few columns per row and the rows are in sorted order.

### What's the benefit of index?

Well-designed indexes can reduce disk I/O operations and consume fewer system resources therefore improving query performance.
Indexes can be helpful for a variety of queries that contain SELECT, UPDATE, DELETE, or MERGE statements.

Index maintenance, rebuild and reorganization ?

 The SQL Server Database Engine automatically maintains indexes whenever insert, update, or delete operations are made to the underlying data. 


Over time these modifications can cause the information in the index to become scattered in the database (fragmented). Fragmentation exists when indexes have pages in which the logical ordering, based on the key value, does not match the physical ordering inside the data file. Heavily fragmented indexes can degrade query performance and cause your application to respond slowly.


You can remedy index fragmentation by reorganizing or rebuilding an index. For partitioned indexes built on a partition scheme, you can use either of these methods on a complete index or a single partition of an index. 

Rebuilding an index drops and re-creates the index. This removes fragmentation, reclaims disk space by compacting the pages based on the specified or existing fill factor setting, and reorders the index rows in contiguous pages. When ALL is specified, all indexes on the table are dropped and rebuilt in a single transaction. Reorganizing an index uses minimal system resources. It defragments the leaf level of clustered and nonclustered indexes on tables and views by physically reordering the leaf-level pages to match the logical, left to right, order of the leaf nodes.

Reorganizing also compacts the index pages. Compaction is based on the existing fill factor value.

### What is clustered index?

A clustered index stores the actual data rows at the leaf level of the index.
An important characteristic of the clustered index is that the indexed values are sorted in either ascending or descending order. 

As a result, there can be only one clustered index on a table or view. In addition, data in a table is sorted only if a clustered index has been defined on a table.

Creating a clustered index on the table actually transforms the table into a b-tree type structure. Your clustered index IS your table it is not separate from the table.


### What is non-clustered index?

Unlike a clustered indexed, the leaf nodes of a nonclustered index contain only the values from the indexed columns and row locators that point to the actual data rows, rather than contain the data rows themselves. This means that the query engine must take an additional step in order to locate the actual data.

A row locator’s structure depends on whether it points to a clustered table or to a heap. If referencing a clustered table, the row locator points to the clustered index, using the value from the clustered index to navigate to the correct data row. If referencing a heap, the row locator points to the actual data row.


You can create more than one nonclustered index per table or view. SQL Server 2005 supports up to 249 nonclustered indexes, and SQL Server 2008 support up to 999.

### Index types?

**Composite index**: An index that contains more than one column. In both SQL Server 2005 and 2008, you can include up to 16 columns in an index, as long as the index doesn’t exceed the 900-byte limit. Both clustered and nonclustered indexes can be composite indexes.
Unique Index: An index that ensures the uniqueness of each value in the indexed column. If the index is a composite, the uniqueness is enforced across the columns as a whole, not on the individual columns. For example, if you were to create an index on the FirstName and LastName columns in a table, the names together must be unique, but the individual names can be duplicated.
A unique index is automatically created when you define a primary key or unique constraint:

**Primary key**: When you define a primary key constraint on one or more columns, SQL Server automatically creates a unique, clustered index if a clustered index does not already exist on the table or view. However, you can override the default behavior and define a unique, nonclustered index on the primary key.
Unique: When you define a unique constraint, SQL Server automatically creates a unique, nonclustered index. You can specify that a unique clustered index be created if a clustered index does not already exist on the table.
Covering index: A type of index that includes all the columns that are needed to process a particular query. For example, your query might retrieve the FirstName and LastName columns from a table, based on a value in the ContactID column. You can create a covering index that includes all three columns.

### Index strategy?

For tables that are heavily updated, use as few columns as possible in the index, and don’t over-index the tables.

If a table contains a lot of data but data modifications are low, use as many indexes as necessary to improve query performance. However, use indexes judiciously on small tables because the query engine might take longer to navigate the index than to perform a table scan.

For clustered indexes, try to keep the length of the indexed columns as short as possible. Ideally, try to implement your clustered indexes on unique columns that do not permit null values. This is why the primary key is often used for the table’s clustered index, although query considerations should also be taken into account when determining which columns should participate in the clustered index.

The uniqueness of values in a column affects index performance. In general, the more duplicate values you have in a column, the more poorly the index performs. On the other hand, the more unique each value, the better the performance. When possible, implement unique indexes.

For composite indexes, take into consideration the order of the columns in the index definition. Columns that will be used in comparison expressions in the WHERE clause (such as WHERE FirstName = 'Charlie') should be listed first. Subsequent columns should be listed based on the uniqueness of their values, with the most unique listed first.

You can also index computed columns if they meet certain requirements. For example, the expression used to generate the values must be deterministic (which means it always returns the same result for a specified set of inputs).

### What is Execution Plan?

An execution plan, simply put, is the result of the query optimizer's attempt to calculate the most efficient way to imple­ment the request represented by the T-SQL query you sub­mitted.
It estimates the work load of a SQL query. It may change the original query, but get the same result.



### Statistics?

SQL Server’s query optimizer uses distribution statistics to determine how it’s going to satisfy your SQL query. These statistics represent the distribution of the data within a column, or columns. The Query Optimizer uses them to estimate how many rows will be returned from a query plan. With no statistics to show how the data is distributed, the optimizer has no way it can compare the efficiency of different plans and so will be frequently forced to simply scan the table or index. Without statistics, it can’t possibly know if the column has the data you’re looking for without stepping through it. With statistics about the column, the optimizer can make much better choices about how it will access your data and use your indexes.

