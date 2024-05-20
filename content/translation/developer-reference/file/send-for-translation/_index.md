---
id: "file-request"
weight: 10
date: "2023-10-20"
author: "Vladimir Lapin"
type: docs
url: /translation/file/request/
productName: "GroupDocs.Translation Cloud"
title: Sending files for translation
description: How to send files for translation to the selected languages.
keywords:
- translate
- send
- input
- request
- file
- document
- content
---

To translate any file, send a **POST** request to the `https://api.groupdocs.cloud/v2.0/translation/auto` GroupDocs.Translation Cloud REST API endpoint. Nevertheless it is highly recommended to use the endpoint, corresponding to your file format. To authorize the request, pass the [access token](/translation/authorization/) in **Authorization** header (_Bearer_ authentication).

The file and translation parameters are provided in JSON format in the request body.

```json
{
  "sourceLanguage": "string",
  "targetLanguages": [
    "string"
  ],
  "file": "string",
  "url": "string",
  "savingMode": "Files",
  "format": "Unknown",
  "outputFormat": "string",
  "masters": false,
  "formatting": true,
  "separator": "string",
  "elements": [
    0
  ],
  "ranges": {
    worksheetIndex: {
      "rows": [
        0
      ],
      "columns": [
        0
      ],
      "ranges": [
        {
          "cellStartIndex": "string",
          "cellEndIndex": "string"
        }
      ]
    }
  },
  "shortcodedict": {
    "shortCodeIndex": [
      "string"
    ]
  },
  "frontMatterList": [
    [
      "string"
    ]
  ]
}
```

{{% alert color="primary" %}} 
Though you have a possibility to provide your file via cURL, please firstly [upload it](/translation/file/upload/) and pass its URL.
{{% /alert %}}

## Evaluation mode

To use GroupDocs.Translation Cloud REST API in [evaluation mode](/translation/evaluation/), send a **POST** request to the endpoint `https://api.groupdocs.cloud/v2.0/translation/document/trial`.

This endpoint does not use the **Authorization** header, so there is no need to generate an access token. Pay attention, that in evaluation mode you can translate only Microsoft Word and PDF files. All other parameters remain the same as in [regular](/translation/subscription/) file translation requests. 

## Translation settings

Property | Type | Default value | Description
-------- | ---- | ------------- | -----------
`sourceLanguage` | String | `en` (English) | [Language code](/translation/languages/) of the source file.
`targetLanguages` | List of strings | _n/a_ | [Language codes](/translation/languages/) into which the file should be translated.
`url` | String | _n/a_ | Link to a file obtained while uploading it.
`format` | String | `format` | Extension of your file, shoud start with **capital letter**, e.g. Docx.
`outputFormat` | String | _n/a_ | Extension of translated file, if it should be converted.
`separator` | String | , | Delimiter in CSV files.
`elements` | List of integers | null | List of 1 based indexes of pages in PDF or Word document, worksheets in Excel spreadsheet or slides in PowerPoint presentation.
`ranges` | Dictionary | nulll | Dictionary of specific ranges in Excel spreadsheet to translate, where the key is the worksheet index and the value is either list of indexes of specific rows or specific columns or tuple of cells indexes.
`masters` | Boolean | false | If master slides in PowerPoint presentation should be translated.
`shortcodedict` | Dictionary | null | Dictionary where the key is short code index and the value is list of strings of parameters names or their indexes in string format.
`frontMatterList` | List | List of list of strings, where each list of strings is the path to a scalar node that requires translation.
`savingMode` | String | Files | If the translated file should be saved as file (Files), archive (Archive) or both (Both).
`formatting` | Boolean | true | If style and layout of PDF file should be preserved, recommended if you need only textual content as works faster.

## Return value

If successful, this method returns JSON with a unique identifier (value of the `id` property) of the translation request in the [queue](/translation/workflow/):

```json
{
	"status": 202,
	"message": "Starting translation",
	"id": "a4fc6c6e-81b0-43c8-b62b-b8bb99520ce9"
}
```

Otherwise, it returns a HTTP status code corresponding to the error.

## What’s next

Translation will take a few seconds, depending on the size of the file, the volume of its textual content and the current GroupDocs.Translation Cloud load. See the article [Fetching translations](/translation/file/fetch/) for information on how to get translations from the server.

## cURL example

{{< tabs "example1" >}}
{{< tab "Request (free tier/paid plan)" >}}
```bash
curl --location --request POST 'https://api.groupdocs.cloud/v2.0/translation/auto' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...UV1hLfgNCSQ4VKGCOA' \
--data '{
  "sourceLanguage": "en",
  "targetLanguages": [
    "de"
  ],
  "url": "https://translation-groupdocs-app.s3.us-west-2.amazonaws.com/0cd7b09d-4d63-4bcd-a9a5-dfd72897aa17.pdf...ff474526313a24821e98",
  "savingMode": "Files",
  "format": "Pdf",
  "outputFormat": "pdf",
  "masters": false,
  "formatting": true,
  "separator": "string",
  "elements": null,
  "ranges": null,
  "shortcodedict": null,
  "frontMatterList": null
}'
```
{{< /tab >}}
{{< tab "Request (evaluation)" >}}
```bash
curl --location --request POST 'https://api.groupdocs.cloud/v2.0/translation/document/trial' \
--header 'Content-Type: application/json' \
--data '{
  "sourceLanguage": "en",
  "targetLanguages": [
    "de"
  ],
  "url": "https://translation-groupdocs-app.s3.us-west-2.amazonaws.com/0cd7b09d-4d63-4bcd-a9a5-dfd72897aa17.pdf...ff474526313a24821e98",
  "savingMode": "Files",
  "format": "Pdf",
  "outputFormat": "pdf",
  "masters": false,
  "formatting": true,
  "separator": "string",
  "elements": null,
  "ranges": null,
  "shortcodedict": null,
  "frontMatterList": null
}'
```
{{< /tab >}}
{{< tab "Response" >}}
```json
{
	"status": 202,
	"message": "Starting translation",
	"id": "a4fc6c6e-81b0-43c8-b62b-b8bb99520ce9"
}
```
{{< /tab >}}
{{< /tabs >}}
