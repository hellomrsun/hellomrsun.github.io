---
layout: post
read_time: true
show_date: true
title:  How to download an Excel file from ASP.NET Web API in Angular application?
date:   2020-10-26 08:00:00 +0100
description: How to download an Excel file from ASP.NET Web API in Angular application?
img: posts/2020-10-06-angular-download/angular.png
tags: [Angular, ASPNET]
author: SUN Jiangong
---

I've looked for some complete solution to download an EXCEL file from an ASP.NET Web API in Angular 9 application, but I didn't find it.

As I've done it recently, I would like to share my implementation with you if it helps.

Firstly, expose an interface in the Web API to download the Excel file.

```csharp
[HttpGet]
[Route("api/v1/excel")]
public async Task<HttpResponseMessage> GenerateExcelFile(){
    try{
        var data = await GetData();
        var stream = _excelGenerationService.Generate(data);
       
        //This is very important, it reset the reading position of the stream!
        stream.Position = 0;

        var result = Request.CreateResponse(HttpStatusCode.OK);
        result.Content = new StreamContent(stream);
        result.Content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
        result.Content.Headers.ContentLength = stream.Length;
        result.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachement");

        return result;
    }
    catch(Exception e){
        _logger.Error("Failed to download excel", e);
        return new HttpResponseMessage(HttpStatusCode.InternalServerError);
    }
}
```

You need to install npm package **file-saver** in your application to save the Excel.

```npm
npm install file-saver --save
```

And then, you can download the content in your Angular application by creating a HTTP GET request.

```typescript

import * as FileSaver from 'file-saver';

downloadExcel(){
    const headers = this.headerService.CreateHeaders();
    const url = environment.api + '/api/v1/excel';
    return this.httpClient.get(url, 
    {
        // You need to set responseType to blob
        'responseType':'blob',
        headers
    }).subscribe((x: Blob) => {
        FileSaver.saveAs(x, 'FileName.xlsx');
    });
}
```

This code works perfectly in IE and Chrome.

Feel free to take it as a sample code. :)
