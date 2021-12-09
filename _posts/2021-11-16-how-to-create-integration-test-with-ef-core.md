---
layout: post
title: How to create integration tests with Entity Framework (EF) core?
description: How to create integration tests with ef core (Entity Framework Core)
excerpt_separator:  <!--more-->
tags: CSharp | Entity-Framework-Core | Entity-Framework
canonical_url: 'https://sunjiangong.com/how-to-create-integration-test-with-entity-framework-core/'
---

It's not easy to create integration test with database, no matter whether you create queries directly against entity framework's DbContext or you create your queries with repositary pattern which operate on your DbSets.

You need to always connect to your database to test your use cases with the real data or fake data you have prepared.

The good news is you can use the EF core's in-memory database provider to tackle it easily.

<!--more-->

Firstly, install the nuget package "Microsoft.EntityFrameworkCore.InMemory".

```cmd
Install-Package Microsoft.EntityFrameworkCore.InMemory -Version 6.0.0
```

Then, you need to create an unique in-memory database instance for each test to prevent data collision in different use cases.

Here I use the builder pattern to create the DbContext initialization helper to use it easily in all my tests.

```csharp
public class TestDBContextBuilder
{
    private readonly TestDBContext _testDbContext;

    public TestDBContextBuilder()
    {
        _testDbContext = null;
        var options = new DbContextOptionsBuilder<TestDBContext>()
                .UseInMemoryDatabase(databaseName: Guid.NewGuid().ToString())
                .Options;
        _testDbContext = new TestDBContext(options);
        _testDbContext.ChangeTracker.QueryTrackingBehavior = QueryTrackingBehavior.NoTracking;
    }

    public TestDBContext Build()
    {
        _testDbContext.SaveChanges();
        return _testDbContext;
    }

    public TestDBContextBuilder WithUsers(IList<User> users)
    {
        _testDbContext.Users.AddRange(users);
        return this;
    }

    public TestDBContextBuilder WithContracts(IList<Contract> contracts)
    {
        _testDbContext.Contracts.AddRange(contracts);
        return this;
    }
}
```

Then, you just need to create your test with the prepared data and test if the code behave as you have expected.

```csharp
[Test]
public async Task Shouw_get_users_ok()
{
    //Arrange
    var users = new List<User>{
        // Code to create users
    };
    // Initialize dbContext with the users
    using var testDbContext = new TestDBContextBuilder().WithUsers(users).Build();
    var uow = new UnitOfWork<TestDBContext>(testDbContext);
    _target = new UserService(uow);

    //Act
    var result = await _target.GetActiveUsers();

    //Assert
    Check.That(result.Count).Equals(10);
}
```

So you have all the tips to create properly the integration tests with EF core.

Hope you enjoyed it!