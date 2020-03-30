---
layout: post
title: How to do Code-First approach with Entity Framework Core and SQL LocalDB
excerpt_separator:  <!--more-->
tags: Entity-Framework Entity-Framework-Core Code-First SqlLocalDb
canonical_url: 'https://sunjiangong.com/Entity-Framework-Core-Code-First-Database-With-SQL-LocalDb/'
---


If you have used Entity Framework, you have probably known that there are 3 possible approaches to work with the database:

* **Database First**

Database First is the most common practice when working an existing database.

In this case, an **.EDMX** (**E**ntity **D**ata **M**odel **X**ML) file will be generated when you map the database in your project. And it contains all the data models.

* **Model First**

With Model First approach, you start by creating .EDMX file with models in the designer, then you generate the database from the .EDMX file.

* **Code First**

With Code First approach, you create the data models firstly, and then generate or update the database with incremental migrations.

You have refined control on the details of data models, like the column constraints(max/min length), relationships etc.

And with the migration history, you can easily move forward or rollback your database version while ensuring the data model consistency.

<!--more-->

<br/>

Here I'll use Code First approach to design, generate, and update my database with Entity Framework Core (EF Core) and SQL LocalDb.

<br/>

### 1. Create SQL LocalDb file.

Go to "**SQL Server Object Explorer -> SQL Server -> (localdb)\MSSQLLocalDB**" in Visual Studio, right-click "**Databases**" and click "**Create Database**".

Specify the database name and its path, and click OK.

![](./../../../assets/images/EfCoreCodeFirstSqlLocalDb/001_create_db.PNG)

<br/>

Once the database is created, two files are created:
* **LDF**: is the Log Database File
* **MDF**: is the Master Database File

![](./../../../assets/images/EfCoreCodeFirstSqlLocalDb/002_db_files.PNG)


<br/>


## 2. Create data model classes

Create data model class "Grape" first with some basic properties like Id, Name and Description.

Id is primary key and auto incremented.

You can also see the its table name and schema name. 

**Note** that the table name in the database could be different from the class model name.

```csharp
[Table("Grape", Schema ="dbo")]
public class Grape
{
    [Key]
    [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
    public int Id { get; set; }

    [MaxLength(100)]
    public string Name { get; set; }

    [MaxLength(255)]
    public string Description { get; set; }
}
```

Once the model is created, we should create the DbContext, which is the mapping of the database.

I'll create a custom WineDbContext, and declare the Grape DbSet in it.

```csharp
public class WineDbContext : DbContext, IDbContext
{
    public DbSet<Grape> Grapes { get; set; }
}
```

But it's not finished about the WineDbContext, I need to initialize the connection to the database.

```csharp
public class WineDbContext : DbContext, IDbContext
{
    public DbSet<Grape> Grapes { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer(CodeFirstUpdateConnectionString);
    }

    private static string CodeFirstUpdateConnectionString
    {
        get
        {
            var config = new ConfigurationBuilder()
                .AddJsonFile(Path.Combine(Environment.CurrentDirectory, "appsettings.json"))
                .Build();
            var result = config.GetSection("ConnectionStrings")["WineDbConnection"];

            return result;
        }
    }
}
```

CodeFirstUpdateConnectionString retrieves the value from configuration file: **appsettings.json**

```json
{
  "ConnectionStrings": {
    "WineDbConnection": "Data Source=(localdb)\\MSSQLLocalDB;Initial Catalog=[AbsoluteFolderPath]\\WINEDB.MDF;Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False"
  }
}
```

<br/>

## 3. Create database migration

You need to install nuget package **Microsoft.EntityFrameworkCore.Tools** in the database project.


![](./../../../assets/images/EfCoreCodeFirstSqlLocalDb/003_install_efcore_tools_package.PNG)


Go to "**Package Manager Console**", and choose the database project as "**Default project**", and create the migration with "**Add-Migration**" command.

```bash
Add-Migration Init
```

![](./../../../assets/images/EfCoreCodeFirstSqlLocalDb/004_create_first_migration.PNG)


The generated class is the following.

You can see there are 2 methods: **Up** and **Down**.

**Up** contains the code will be executed when you run this migration against the database.

And **Down** contains the code will be executed when you rollback this migration.

```csharp
public partial class Init : Migration
{
    protected override void Up(MigrationBuilder migrationBuilder)
    {
        migrationBuilder.EnsureSchema(
            name: "dbo");

        migrationBuilder.CreateTable(
            name: "Grape",
            schema: "dbo",
            columns: table => new
            {
                Id = table.Column<int>(nullable: false)
                    .Annotation("SqlServer:Identity", "1, 1"),
                Name = table.Column<string>(maxLength: 100, nullable: true),
                Description = table.Column<string>(maxLength: 255, nullable: true)
            },
            constraints: table =>
            {
                table.PrimaryKey("PK_Grape", x => x.Id);
            });
    }

    protected override void Down(MigrationBuilder migrationBuilder)
    {
        migrationBuilder.DropTable(
            name: "Grape",
            schema: "dbo");
    }
}
```

<br/>

## 4. Update database with migration

Once the migration is ready, you can update the database with it.

To update the database, you need the command:

```bash
Update-Database
```

![](./../../../assets/images/EfCoreCodeFirstSqlLocalDb/005_update_database_with_migration.PNG)

or specifically with the migration name:

```bash
Update-Database -Migration 20200330171646_Init
```

![](./../../../assets/images/EfCoreCodeFirstSqlLocalDb/006_update_database_with_specific_migration.PNG)


<br/>

To debug your code, in case of error, when you execute the commands in Package Manager Console, you can use the following code:

```csharp
#if DEBUG
    if (System.Diagnostics.Debugger.IsAttached == false)
    {
        System.Diagnostics.Debugger.Launch();
    }
#endif
```

<br/>

## 5. Check database

As the migration has beed executed against the database, let's check the database.

You can see here are two tables:
* [dbo].[__EFMigrationsHistory]
* [dbo].[Grape]


![](./../../../assets/images/EfCoreCodeFirstSqlLocalDb/007_database_EfMigrationHistory.PNG)

<br/>

**[dbo].[__EFMigrationsHistory]** is the migration history table, it garantees the database consistency.


![](./../../../assets/images/EfCoreCodeFirstSqlLocalDb/008_EfMigrationHistory.PNG)


<br/>

**[dbo].[Grape]** is Grape table.

![](./../../../assets/images/EfCoreCodeFirstSqlLocalDb/009_Grape.PNG)


<br/>

Now we've seen the code first approach with EF core and SQL LocalDb.

You can see the source project: [HERE](https://github.com/hellomrsun/DotNetCoreAngularSignalRDemo/tree/master/SignalrDotnetCoreApi/SignalrDotnetCoreApi)