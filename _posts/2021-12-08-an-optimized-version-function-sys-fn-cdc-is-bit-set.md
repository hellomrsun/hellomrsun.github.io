---
layout: post
read_time: true
show_date: true
title:  An optimized version of function sys.fn_cdc_is_bit_set
date:   2021-12-08 08:00:00 +0100
description: An optimized version of function sys.fn_cdc_is_bit_set, Change Data Capture Table, update_mask
img: posts/2021-12-08-cdc-is-bit-set/cdc.jpg 
tags: [SqlServer, SQL]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/optimized-version-function-sys-fn-cdc-is-bit-set.html'
---

Change Data Capture (CDC) table uses __$update_mask to track the modifications of ordinal columns.

__$update_mask's type is varbinary(128)

The function **sys.fn_cdc_is_bit_set** is provided within Microsoft SQL Server. It is used to calculate if the value of a column is modified, based on the column's position and the __$update_mask.

<!--more-->

![](./../../../assets/img/posts/2021-12-08-cdc-is-bit-set/cdc.jpg)

<br />

Its signature is:

```sql
sys.fn_cdc_is_bit_set(position, update_mask)
```

But the function **sys.fn_cdc_is_bit_set** provided in SQL Server is not optimal when there are a lot of data to process.

Here is an optimal version:

```sql
CREATE FUNCTION [dbo].[fn_cdc_is_bit_set_optimized]
(
    @position INT,
    @update_mask VARBINARY(128)
)
RETURNS BIT
AS
BEGIN
    DECLARE @isSet BIT =
        CASE WHEN SUBSTRING(@update_mask,DATALENGTH(@update_mask) - ((@position-1)/8),1) & POWER(2, (@position-1)%8) > 0
        THEN 1 ELSE 0 END
    RETURN @isSet;
END
```
