---
layout: post
title: How to upload and download file in Angular 5+ and .net core
description: How to upload and download file in Angular 5+ and .net core
excerpt_separator:  <!--more-->
tags: Angular, CSharp
canonical_url: 'https://sunjiangong.com/how-to-upload-and-download-file-in-angular-and-dotnet-core/'
---

When you develop a web application in Angular for the front-end and C# or Java in the back-end, it's frequently that you need to upload and download files.

Here is an example that may inspire you in your development.

```html
<!-- Upload file -->
<input hidden #feeFile type="file" #uploader (change)="uploadFees($event)" accept=".xlsx, .xls" />
<button mat-button color="primary" (click)="uploader.click()">
  <mat-icon matTooltip="Upload fees" class="import-export-button">cloud_upload</mat-icon>
</button>
<!-- Download file -->
<button mat-button color="primary" (click)="downloadFees()">
  <mat-icon matTooltip="Download fees" class="import-export-button">cloud_download</mat-icon>
</button>
```

<!--more-->

Define a file object to use in file download and upload.

```typescript
export class DocumentDTO {
  fileName!: string;
  fileData!: string;
  contentType!: string;
}
```

Define a HHTML input event to pass the file.

```typescript
interface HTMLInputEvent extends Event {
  target: HTMLInputElement & EventTarget;
}
```

Define a file service to treat the file.

```typescript
import { Injectable } from '@angular/core';
import { DocumentDTO } from '@app/models/document.model';
import * as FileSaver from 'file-saver';
import { Subject } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class FileService {

  constructor() { }

  saveFile(document: DocumentDTO) {
    //Convert file content to blob
    let blob = this.convertBase64StringToBlob(document.fileData, document.contentType);
    //Save file
    FileSaver.saveAs(blob, document.fileName);
  }

  readFile(file: File): Promise<string> {
    //Convert file to string
    const sub = new Subject<string>();
    const reader = new FileReader();
    reader.onloadend = function () {
      const content: string = reader.result as string;
      sub.next(content);
      sub.complete();
    };
    reader.readAsDataURL(file);
    return sub.asObservable().toPromise();
  }

  private convertBase64StringToBlob(base64: string, contentType: string): Blob {
    const byteCharacters = atob(base64);
    const byteNumbers = new Array(byteCharacters.length);
    for (let i = 0; i < byteCharacters.length; i++) {
      byteNumbers[i] = byteCharacters.charCodeAt(i);
    }
    const byteArray = new Uint8Array(byteNumbers);
    return new Blob([byteArray], { type: contentType });
  }
}
```

Typescript code to upload and download Excel file.

```typescript
async uploadFee(e: any) {
  let target = e.target as HTMLInputElement;
  const file = (target.files as FileList)[0];
  var fileContent = await this.fileService.readFile(file);
  let document = this.createDocumentDto(file, fileContent);

  //Upload file by calling web api upload file endpoint
  await this.http.post<boolean>(`${this.apiUrl}/document`, document).toPromise();

  //reset feeFile value to be able to reload the same file
  this.feeFile.nativeElement.value = null;
}

private createDocumentDto(file: File, content: string): DocumentDTO {
  let doc = new DocumentDTO();
  doc.fileName = file.name;
  doc.contentType = file.type;
  doc.fileData = content;
  return doc;
}

async downloadFees() {
  let queryParams = this.createFilterParams(this.filter);
  let document = await this.http.get<DocumentDTO>(`${this.apiUrl}/document`, { params: queryParams }).toPromise();
  this.fileService.saveFile(document);
}

private createFilterParams(filter: CodeDDGFilterDTO) {
  let queryParams = new HttpParams();
  if (filter.Name !== undefined) queryParams = queryParams.set("Name", filter.Name);
  if (filter.Code !== undefined) queryParams = queryParams.set("Code", filter.Code);
  return queryParams;
}
```

Back-end code in .net core web api.

```csharp
[HttpPost]
[Route("document")]
public async Task<bool> UploadFeesExcelAsync(DocumentDTO document)
{
  return await _feesImporter.ImportDocument(document);
}

[HttpGet]
[Route("document")]
public async Task<DocumentDTO> DownloadFeesExcelAsync([FromQuery] FilterDTO filter)
{
  return await _feesExporter.GenerateDocument(filter);
}
```

Ok, you have seen the sample code. You can make your hands dirty now. :)