---
id: "languages"
weight: 30
date: "2023-10-20"
author: "Vladimir Lapin"
type: docs
url: /translation/languages/
productName: "GroupDocs.Translation Cloud"
title: Getting supported languages
description: How to get a full list of supported language pairs.
keywords:
- languages
- source
- target
- pairs
---

To get a list of all translation language pairs [supported](/translation/translation-languages/) by GroupDocs.Translation Cloud, send a **GET** request to `https://api.groupdocs.cloud/v2.0/translation/languages` REST API endpoint.

{{% alert color="primary" %}} 
This request does not require authorization.
{{% /alert %}}

The list of all supported language pairs (as an array of objects) is returned in JSON format in the response body.

Property | Type | Description
-------- | ---- | -----------
`source` | String | Source language (translate from) represented by its [ISO 639-1 code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).
`targets` | Array of strings | One or more target languages (translate to) represented by their [ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).

## Example

```json
[
	{
		"source": "en",
		"targets": [
			"ru",
			"de",
			"fr",
			"zh",
			"es",
			"it",
			"ar",
			"pt",
			"pl",
			"uk",
			"vi",
			"id",
			"hi",
			"el",
			"nl",
			"hu",
			"sv",
			"tr",
			"ko",
			"ja",
			"fi",
			"cs",
			"ga",
			"sk",
			"fa",
			"az",
			"he",
			"th",
			"ro",
			"ms",
			"bg",
			"bn",
			"no",
			"da",
			"lv",
			"lt",
			"et",
			"hy",
			"ca",
			"hr",
			"sr",
			"af",
			"ur",
			"tl",
			"ka"
		]
	},
	...,
	{
		"source": "ka",
		"targets": [
			"en"
		]
	}
]
```