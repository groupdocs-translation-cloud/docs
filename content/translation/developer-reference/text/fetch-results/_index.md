---
id: "text-fetch"
weight: 20
date: "2023-10-20"
author: "Vladimir Lapin"
type: docs
url: /translation/text/fetch/
productName: "GroupDocs.Translation Cloud"
title: Fetching translations
description: How to fetch the translated text from the GroupDocs.Translation Cloud queue.
keywords:
- translate
- text
- content
- queue
- get
- obtain
- fetch
- result
---

When text is submitted for translation, it is queued to ensure a stable response even under high load. To obtain the translations, send a **GET** request to the `https://api.groupdocs.cloud/v2.0/translation/text/{request ID}` GroupDocs.Translation Cloud REST API endpoint. To authorize the request, pass the [access token](/translation/authorization/) in **Authorization** header (_Bearer_ authentication).

Provide the [unique identifier](/translation/text/request/#return-value) of the translation task:

```bash
curl --request GET --location 'https://api.groupdocs.cloud/v2.0/translation/text/a4fc6c6e-81b0-43c8-b62b-b8bb99520ce9' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...UV1hLfgNCSQ4VKGCOA'
```

## Translated texts

Translations are returned in JSON format in the response body.

```json
{
	"status": 200,
	"message": "Text translated successfully",
	"translations": {
		"de": [
			"Hallo, Welt! Ich kann diesen Text in meiner Sprache lesen."
		]
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
`translations` | Dictionary | Translations as a key-value list:<ul><li>Key is the [language code](/translation/languages/) into which the texts were translated.</li><li>Value is the array of translated strings corresponding to the [source texts](/translation/text/request/#translation-settings).</li></ul>

If the text is not yet translated, try fetching the result in a couple of seconds using the same ID.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request GET --location 'https://api.groupdocs.cloud/v2.0/translation/text/a4fc6c6e-81b0-43c8-b62b-b8bb99520ce9' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...UV1hLfgNCSQ4VKGCOA'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```json
{
	"status": 200,
	"message": "Text translated successfully",
	"translations": {
		"uk": [
			"Я можу прочитати цей вірш своєю мовою."
		],
		"ja": [
			"\"ハローワールド!この文章は,私の言語で読める."
		]
	}
}
```
{{< /tab >}}
{{< /tabs >}}
