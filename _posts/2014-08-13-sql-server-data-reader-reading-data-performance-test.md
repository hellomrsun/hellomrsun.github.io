---
layout: post
# title: SQL Server data reader reading data performance test
# description: SQL Server data reader reading data performance test
# excerpt_separator:  <!--more-->
# tags: Performance | SQL-Server
# canonical_url: 'https://sunjiangong.com/sql-server-data-reader-reading-data-performance-test/'
read_time: true
show_date: true
title:  SQL Server data reader reading data performance test
date:   2014-08-13 08:00:00 +0100
description: SQL Server data reader reading data performance test
img: posts/uncategorized/sqlserver.PNG
tags: [Performance, SQLServer]
author: SUN Jiangong
# github:  hellomrsun
mathjax: yes
---


As I've manipulated a lot of data using SQL data reader in recent project. And people says it's not good to access the data by column name.

So I've made an performance test in reading data from SQL data reader.

<!--more-->


Firstly, I've created a table with different data types, like int, varchar, date time etc.


```sql
CREATE TABLE UserInformation(
    Id BIGINT, FirstName NVARCHAR(255), 
    LastName NVARCHAR(255), 
    ValidDate DATETIME, 
    Identification UNIQUEIDENTIFIER)
```

<br/>

Then, I've filled the table with 9024728 lines data. 
Why is it the exact number? It's because the sql server management studio crashes after 9024728 lines' insertion. :-)


Then, I'll use 3 methods to read the **9 millions** lines data.

<br/>

#### Method 1: Get data by column index

```csharp
public void DataReaderGetDataByColumnIndex()
{
    using (_dbConnection)
    {
        var sqlCommand = new SqlCommand(_commandText, _dbConnection);

        _dbConnection.Open();

        SqlDataReader reader = sqlCommand.ExecuteReader();

        var user = new UserInformationEntity();

        _GetByIndexTime.Start();
        while (reader.Read())
        {
            user.Id = reader.GetInt64(0);
            user.FirstName = reader.GetString(1);
            user.LastName = reader.GetString(2);
            user.ValidDate = reader.GetDateTime(3);
            user.Identification = reader.GetGuid(4);
        }
        _GetByIndexTime.Stop();
        Console.WriteLine(string.Format("GetByIndexTime total time:{0}", _GetByIndexTime.Elapsed));
        _dbConnection.Close();
    }
}
```

<br/>

#### Method 2: Get data by column name

```csharp
public void DataReaderGetDataByColumnName()
{
    using (_dbConnection)
    {
        var sqlCommand = new SqlCommand(_commandText, _dbConnection);

        _dbConnection.Open();

        SqlDataReader reader = sqlCommand.ExecuteReader();

        var user = new UserInformationEntity();

        _GetByNameTime.Start();
        while (reader.Read())
        {
            user.Id = Convert.ToInt64(reader["Id"]);
            user.FirstName = reader["FirstName"].ToString();
            user.LastName = reader["LastName"].ToString();
            user.ValidDate = Convert.ToDateTime(reader["ValidDate"]);
            user.Identification = new Guid(reader["Identification"].ToString());
        }
        _GetByNameTime.Stop();
        Console.WriteLine(string.Format("GetByNameTime total time:{0}", _GetByNameTime.Elapsed));
        _dbConnection.Close();
    }
}
```

<br/>

#### Method 3: Get column ordinal by column name, then Get data by column ordinal

```csharp
public void DataReaderGetColumnIndexByColumnNameThenGetData()
{
    using (_dbConnection)
    {
        var sqlCommand = new SqlCommand(_commandText, _dbConnection);

        _dbConnection.Open();

        SqlDataReader reader = sqlCommand.ExecuteReader();

        var user = new UserInformationEntity();

        var id = reader.GetOrdinal("Id");
        var firstName = reader.GetOrdinal("FirstName");
        var lastName = reader.GetOrdinal("LastName");
        var validDate = reader.GetOrdinal("ValidDate");
        var identification = reader.GetOrdinal("Identification");

        _GetByNameThenIndexTime.Start();
        while (reader.Read())
        {
            user.Id = reader.GetInt64(id);
            user.FirstName = reader.GetString(firstName);
            user.LastName = reader.GetString(lastName);
            user.ValidDate = reader.GetDateTime(validDate);
            user.Identification = reader.GetGuid(identification);
        }
        _GetByNameThenIndexTime.Stop();
        Console.WriteLine(string.Format("GetByNameThenIndexTime total time:{0}", _GetByNameThenIndexTime.Elapsed));
        _dbConnection.Close();
    }
}
```

When I run the program to get the execution time:


![](./../../../assets/img/posts/2014-08-13-SqlReaderPerformance/01.png)


You can see that Method1 and Method3 has almost the same result, and Method2 are about 3 times longer.


So the prefered approach will be the third one.


Enjoy coding!