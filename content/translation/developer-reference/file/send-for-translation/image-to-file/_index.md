---
id: "image-to-file-request"
weight: 40
date: "2023-10-20"
author: "Vladimir Lapin"
type: docs
url: /translation/file/request/image-to-file/
productName: "GroupDocs.Translation Cloud"
title: Sending images and scanned PDFs for translation
description: How to scans and image files for translation to the selected languages.
keywords:
- translate
- send
- input
- request
- file
- pdf
- image
- document
- content
---

To translate scanned PDF or image file and get result as PDF, send a **POST** request to the `https://api.groupdocs.cloud/v2.0/translation/image-to-file` GroupDocs.Translation Cloud REST API endpoint. To authorize the request, pass the [access token](/translation/authorization/) in **Authorization** header (_Bearer_ authentication).

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
  "ocrformat": "Pdf",
  "outputFormat": "string",
  "rotationAngle": 0,
  "formatting": true,
  "pages": [
    0
  ]
}
```

{{% alert color="primary" %}} 
Though you have a possibility to provide your file via cURL, please firstly [upload it](/translation/file/upload/) and pass its URL.
{{% /alert %}}

## Evaluation mode

Evaluation mode is not available for scans and image files, kindly register account and try image translation with provided free credits.

## Translation settings

Property | Type | Default value | Description
-------- | ---- | ------------- | -----------
`sourceLanguage` | String | `en` (English) | [Language code](/translation/languages/) of the source file.
`targetLanguages` | List of strings | _n/a_ | [Language codes](/translation/languages/) into which the file should be translated.
`url` | String | _n/a_ | Link to a file obtained while uploading it.
`format` | String | `Unknown` | Extension of your file, shoud start with **capital letter**, e.g. Docx.
`ocrformat` | String | `Pdf` | Format of file after text recognition of image, put `Xlsx` if you are translating scanned tables, otherwise leace `Pdf`.
`outputFormat` | String | _n/a_ | Extension of translated file, if it should be converted.
`pages` | List of integers | null | List of 1 based indexes of pages in PDF scan.
`rotationAngle` | Integer | null | Though skew correction is used, when the rotation angle is quite large (>15°) you should pass it manually.
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
curl --location --request POST 'https://api.groupdocs.cloud/v2.0/translation/image-to-file' \
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
  "ocrformat": "Pdf",
  "outputFormat": "pdf",
  "formatting": true,
  "rotationAngle": 0,
  "pages": null
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
