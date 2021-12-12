---
layout: post
read_time: true
show_date: true
title:  Which library to generate Excel in C#? OpenXmlSdk or ClosedXml?
date:   2020-10-05 08:00:00 +0100
description: Which library to generate Excel in C#? OpenXmlSdk or ClosedXml? CSharp, Excel generation
img: posts/2020-10-05-excel-generation/closedxml.png
tags: [Excel, CSharp]
author: SUN Jiangong
---

I need to generate Excel files in my recent work. The file is not huge and it's around 5000 lines.

I have tried two open source libraries to generate them. 

They are: 
- **OpenXmlSdk**
- **ClosedXml**

There is very good library **EPPlus** which is very popular. It has become a commercial product since the version 5, so a license is required for commercial use. I work for a French bank, and I prefer to use an open source library because of the long purchase procedure in the bank and the cost.

So here, I just compare the OpenXmlSdk and ClosedXml.


### 1. OpenXmlSdk

OpenXmlSdk is a SDK developed by Microsoft [SDK](https://github.com/OfficeDev/Open-XML-SDK){:target="_blank"} to manipulate different types of file like Excel, PowerPoint etc.

You can download its nuget package: [DocumentFormat.OpenXml](https://www.nuget.org/packages/DocumentFormat.OpenXml/){:target="_blank"}

```quote
The Open XML SDK provides tools for working with Office Word, Excel, and PowerPoint documents. It supports scenarios such as:

- High-performance generation of word-processing documents, spreadsheets, and presentations.
- Populating content in Word files from an XML data source.
- Splitting up (shredding) a Word or PowerPoint file into multiple files, and combining multiple Word/PowerPoint files into a single file.
- Extraction of data from Excel documents.
- Searching and replacing content in Word/PowerPoint using regular expressions.
- Updating cached data and embedded spreadsheets for charts in Word/PowerPoint.
- Document modification, such as adding, updating, and removing content and metadata.
```

You can create an Excel document with the following sample code:

```csharp
public static void CreateSpreadsheetWorkbook(string filepath)
{
    // Create a spreadsheet document by supplying the filepath.
    // By default, AutoSave = true, Editable = true, and Type = xlsx.
    SpreadsheetDocument spreadsheetDocument = SpreadsheetDocument.Create(filepath, SpreadsheetDocumentType.Workbook);

    // Add a WorkbookPart to the document.
    WorkbookPart workbookpart = spreadsheetDocument.AddWorkbookPart();
    workbookpart.Workbook = new Workbook();

    // Add a WorksheetPart to the WorkbookPart.
    WorksheetPart worksheetPart = workbookpart.AddNewPart<WorksheetPart>();
    worksheetPart.Worksheet = new Worksheet(new SheetData());

    // Add Sheets to the Workbook.
    Sheets sheets = spreadsheetDocument.WorkbookPart.Workbook.
        AppendChild<Sheets>(new Sheets());

    // Append a new worksheet and associate it with the workbook.
    Sheet sheet = new Sheet() { Id = spreadsheetDocument.WorkbookPart.
        GetIdOfPart(worksheetPart), SheetId = 1, Name = "mySheet" };
    sheets.Append(sheet);

    workbookpart.Workbook.Save();

    // Close the document.
    spreadsheetDocument.Close();
}
```

It seems ok to initialize a Excel file with a worksheet with the above code. But it becomes a little complicated when you want to insert data into it.

You need to insert each row and then each cell into the worksheet before write any data.

Here is some sample code to initialize a row and a cell.

```csharp
// Given a column name, a row index, and a WorksheetPart, inserts a cell into the worksheet. 
// If the cell already exists, returns it. 
private static Cell InsertCellInWorksheet(string columnName, uint rowIndex, WorksheetPart worksheetPart)
{
    Worksheet worksheet = worksheetPart.Worksheet;
    SheetData sheetData = worksheet.GetFirstChild<SheetData>();
    string cellReference = columnName + rowIndex;

    // If the worksheet does not contain a row with the specified row index, insert one.
    Row row;
    if (sheetData.Elements<Row>().Where(r => r.RowIndex == rowIndex).Count() != 0)
    {
        row = sheetData.Elements<Row>().Where(r => r.RowIndex == rowIndex).First();
    }
    else
    {
        row = new Row() { RowIndex = rowIndex };
        sheetData.Append(row);
    }

    // If there is not a cell with the specified column name, insert one.  
    if (row.Elements<Cell>().Where(c => c.CellReference.Value == columnName + rowIndex).Count() > 0)
    {
        return row.Elements<Cell>().Where(c => c.CellReference.Value == cellReference).First();
    }
    else
    {
        // Cells must be in sequential order according to CellReference. Determine where to insert the new cell.
        Cell refCell = null;
        foreach (Cell cell in row.Elements<Cell>())
        {
            if (cell.CellReference.Value.Length == cellReference.Length)
            {
                if (string.Compare(cell.CellReference.Value, cellReference, true) > 0)
                {
                refCell = cell;
                break;
                }
            }
        }

        Cell newCell = new Cell() { CellReference = cellReference };
        row.InsertBefore(newCell, refCell);

        worksheet.Save();
        return newCell;
    }
}
```

Then to write data to the cell, you can use the following code:

```csharp
var cell1 = InsertCellInWorksheet("A", 1, worksheetPart);
cell1.CellValue = new CellValue("Cell Text Value");
cell1.DataType = new EnumValue<CellValues>(CellValues.String);

var cell2 = InsertCellInWorksheet("B", 1, worksheetPart);
var number = 1.2m;
cell2.CellValue = new CellValue(number.ToString());
cell2.DataType = new EnumValue<CellValues>(CellValues.Number);
```

But when you write data in this way, you have to create all cells before. It's quite time consuming and you could create wrong types of cells which could cause Format error.

I would say I've met some problems in my try of this library, and the integration process was not smooth. There are not so much documentation and sample code about this library.

I wanted to find another library which is easier to use and understand.

Then, I tried ClosedXml, and the result is satisfying.


### 2. ClosedXML

[ClosedXML](https://github.com/ClosedXML/ClosedXML){:target="_blank"} is an open source library created based on OpenXmlSdk. It's more user friendly.

You can download its nuget package: [ClosedXMl](https://www.nuget.org/packages/ClosedXML/){:target="_blank"}

```quote
ClosedXML is a .NET library for reading, manipulating and writing Excel 2007+ (.xlsx, .xlsm) files. It aims to provide an intuitive and user-friendly interface to dealing with the underlying OpenXML API.
```

It's very easy to create an Excel.

```csharp
// Create an Excel with one spreasheet
var wb = new XLWorkbook();
var ws = wb.Worksheets.Add("Sheet 1");
wb.SaveAs("SingleSheet.xlsx");

// Create an Excel with multiple spreasheets
var workbook = new XLWorkbook();
foreach (var wsNum in Enumerable.Range(1, 5))
{
  var ws = workbook.Worksheets.Add("Sheet " + wsNum.ToString());
}
workbook.SaveAs("MultipleSheets.xlsx");
```

There are some sample code to insert data in Excel from a string list, array list, object list or DataTable. 

You don't need to initialize each row and cell anymore. ClosedXML has done all that for you behind the scenes. And this could save you a lot of time and energy.

```csharp
// From a list of strings
var listOfStrings = new List<String>();
listOfStrings.Add("House");
listOfStrings.Add("Car");
ws.Cell(1, 1).Value = "From Strings";
ws.Cell(1, 1).AsRange().AddToNamed("Titles");
var rangeWithStrings = ws.Cell(2, 1).InsertData(listOfStrings);

// From a list of arrays
var listOfArr = new List<Int32[]>();
listOfArr.Add(new Int32[] { 1, 2, 3 });
listOfArr.Add(new Int32[] { 1 });
listOfArr.Add(new Int32[] { 1, 2, 3, 4, 5, 6 });
ws.Cell(1, 3).Value = "From Arrays";
ws.Range(1, 3, 1, 8).Merge().AddToNamed("Titles");
var rangeWithArrays = ws.Cell(2, 3).InsertData(listOfArr);

// From a query
var list = new List<Person>();
list.Add(new Person() { Name = "John", Age = 30, House = "On Elm St."   });
list.Add(new Person() { Name = "Mary", Age = 15, House = "On Main St."  });
list.Add(new Person() { Name = "Luis", Age = 21, House = "On 23rd St."  });
list.Add(new Person() { Name = "Henry", Age = 45, House = "On 5th Ave." });

var people = from p in list
where p.Age >= 21
select new { p.Name, p.House, p.Age };

ws.Cell(6, 6).Value = "From Query";
var rangeWithPeople = ws.Cell(7, 6).InsertData(people.AsEnumerable());

// From a DataTable
var dataTable = GetTable();
ws.Cell(6, 1).Value = "From DataTable";
ws.Range(6, 1, 6, 4).Merge().AddToNamed("Titles");
var rangeWithData = ws.Cell(7, 1).InsertData(dataTable.AsEnumerable());
```

For more examples, you can have a look at its GitHub [WIKI](https://github.com/ClosedXML/ClosedXML/wiki){:target="_blank"} page.


Finally, I've used ClosedXML after having tried the two libraries.

Conclusion:
- OpenXmlSdk is truly powerful, but need more profound knowledge about the framework to start with. 
- ClosedXML is a library based on OpenXmlSdk, which is easier to use with a lot of sample codes.
