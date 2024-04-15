---
id: "file-upload"
weight: 10
date: "2023-11-01"
author: "Vladimir Lapin"
type: docs
url: /translation/file/upload/
productName: "GroupDocs.Translation Cloud"
title: Upload file
description: How to upload file to Cloud storage.
keywords:
- translate
- file
- content
- queue
- upload
---
Before starting the translation process, you should upload your file to Cloud S3 storage and only then send request to translate it. To do this, send **POST** request to `https://api.groupdocs.cloud/v2.0/translation/file/upload` GroupDocs.Translation Cloud REST API endpoint. This request doesn't require authorization. 

You should provide a local path to your file in JSON format in the request body.

```json
{
	"path": "/path/to/myfile.pdf"
}
```
As a result, you will receive URL to your file, that you should provide in translation request body.


## cURL example

```bash
curl --location --request POST 'https://api.groupdocs.cloud/v2.0/translation/file/upload' \
--header 'Content-Type: application/json' \
--data '{
	"path": "/path/to/myfile.pdf"
}'
```
