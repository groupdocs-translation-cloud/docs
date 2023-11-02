---
id: "text-request"
weight: 10
date: "2023-10-20"
author: "Vladimir Lapin"
type: docs
url: /translation/text/request/
productName: "GroupDocs.Translation Cloud"
title: Sending texts for translation
description: How to send texts for translation to the selected languages.
keywords:
- translate
- send
- input
- request
- text
- content
---

To translate plain text, send a **POST** request to the `https://api.groupdocs.cloud/v2.0/translation/text` GroupDocs.Translation Cloud REST API endpoint. To authorize the request, pass the [access token](/translation/authorization/) in **Authorization** header (_Bearer_ authentication).

The text and translation parameters are provided in JSON format in the request body.

```json
{
	"sourceLanguage": "en",
	"targetLanguages": [
		"de"
	],
	"containsMarkdown": false,
	"texts": [
		"Hello, world! I can read this text in my language."
	],
}
```

{{% alert color="primary" %}} 
If the translated text is very long, you may encounter an error when calling translation via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Translation settings

Property | Type | Default value | Description
-------- | ---- | ------------- | -----------
`sourceLanguage` | String | `en` (English) | [Language code](/translation/languages/) of the source text.
`targetLanguages` | Array of strings | _n/a_ | [Language codes](/translation/languages/) into which the text should be translated.
`containsMarkdown` | Boolean | `false` | Set to `true` to respect [basic markdown syntax](https://www.markdownguide.org/basic-syntax/) in source text and keep it in the translations (if possible). Otherwise, these symbols will be translated as part of the content.
`texts` | Array of strings | _n/a_ | Texts to be translated.

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

Translation will take a few seconds, depending on the size of the text and the current GroupDocs.Translation Cloud load. See the article [Fetching translations](/translation/text/fetch/) for information on how to get translations from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location --request POST 'https://api.groupdocs.cloud/v2.0/translation/text' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...UV1hLfgNCSQ4VKGCOA' \
--data '{
	"sourceLanguage": "en",
	"targetLanguages": [
		"de"
	],
	"texts": [
		"Hello, world! I can read this text in my language."
	]
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```json
{
	"status": 202,
	"message": "Starting translation",
	"id": "a4fc6c6e-81b0-43c8-b62b-b8bb99520ce9"
}
```
{{< /tab >}}
{{< /tabs >}}
