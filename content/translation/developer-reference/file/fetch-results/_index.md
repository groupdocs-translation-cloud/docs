---
id: "file-fetch"
weight: 30
date: "2023-11-01"
author: "Vladimir Lapin"
type: docs
url: /translation/file/fetch/
productName: "GroupDocs.Translation Cloud"
title: Fetching file translations
description: How to fetch the translated file from the GroupDocs.Translation Cloud queue.
keywords:
- translate
- file
- document
- content
- queue
- get
- obtain
- fetch
- result
---

When file is submitted for translation, it is queued to ensure a stable response even under high load. To obtain the translation, send a **GET** request to the `https://api.groupdocs.cloud/v2.0/translation/document/{request ID}` GroupDocs.Translation Cloud REST API endpoint. To authorize the request, pass the [access token](/translation/authorization/) in **Authorization** header (_Bearer_ authentication).

Provide the [unique identifier](/translation/text/request/#return-value) of the translation task:

```bash
curl --request GET --location 'https://api.groupdocs.cloud/v2.0/translation/document/a4fc6c6e-81b0-43c8-b62b-b8bb99520ce9' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...UV1hLfgNCSQ4VKGCOA'
```

## Evaluation mode

To get the translation from [evaluation](/translation/file/request/#evaluation-mode) request, send a **GET** request to the endpoint `https://api.groupdocs.cloud/v2.0/translation/document/trial/{request ID}`.

This endpoint does not use the **Authorization** header, so there is no need to generate an access token.

You can also use the standard (authorized) endpoint to fetch a translation, even if it was requested in evaluation mode.

## Translated files

Translations are returned in JSON format in the response body.

```json
{
	"status": 200,
	"message": "Pdf document translated by 100%",
	"urls": {
		"de": {
			"url": "https://translation-groupdocs-app.s3.us-west-2.amazonaws.com/0cd7b09d-4d63-4bcd-a9a5-dfd72897aa17.pdf...ff474526313a24821e98",
			"size": 34564
		}
	}
}
```

{{% alert color="primary" %}} 
Translations are stored in the GroupDocs cloud and can be obtained by the task ID within **24 hours** after the text was sent for translation.
{{% /alert %}}

Property | Type | Description
-------- | ---- | -----------
`status` | Number | HTTP response status code.
`message` | String | Verbose status message.
`urls` | Dictionary | Translations as a key-value list:<ul><li>Key is the [language code](/translation/languages/) into which the files were translated.</li><li>Value contains URL of the translated files and their volume.</li></ul>

If the file is not yet translated, try fetching the result in a couple of seconds using the same ID.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request GET --location 'https://api.groupdocs.cloud/v2.0/translation/document/a4fc6c6e-81b0-43c8-b62b-b8bb99520ce9' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...UV1hLfgNCSQ4VKGCOA'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```json
{
	"status": 200,
	"message": "Pdf document translated by 100%",
	"urls": {
		"de": {
			"url": "https://translation-groupdocs-app.s3.us-west-2.amazonaws.com/0cd7b09d-4d63-4bcd-a9a5-dfd72897aa17.pdf...ff474526313a24821e98",
			"size": 34564
		}
	}
}
```
{{< /tab >}}
{{< /tabs >}}
