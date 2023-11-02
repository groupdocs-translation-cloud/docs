---
id: "hello-world"
weight: 40
date: "2023-10-06"
author: "Vladimir Lapin"
type: docs
url: translation/hello-world
aliases:
- translation/quickstart
productName: "GroupDocs.Translation Cloud"
title: Hello, world!
description: Get familiar with GroupDocs.Translation Cloud by running a bare minimum example.
keywords:
- hello world
- evaluation
- example
- sample
- dummies
- code
---

In this article, you will learn how to translate a short text from English to German using GroupDocs.Translation Cloud REST API.

{{% alert color="primary" %}} 
We assume that you have already [signed up](/translation/sign-up/) to the service and have not yet exceeded your [free subscription plan](/translation/subscription/) limits.
{{% /alert %}} 

## You will need

- [Any system](/translation/system-requirements/) with Internet connection.
- A web browser.
- Any tool that allows you to make REST API calls, such as [cURL](https://curl.se/) or [Postman](https://www.postman.com/). The article provides cURL examples.
- **10 minutes** of spare time.

## Getting an access token

The GroupDocs.Translation Cloud API is fully compliant with industry security standards and best practices. Data transfer is carried out using JWT authentication, which eliminates all possibilities of data theft or disclosure.

To obtain a JWT token, get the _Client ID_ and _Client Secret_ credentials:

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.groupdocs.cloud/).
2. Go to [**Applications**](https://dashboard.groupdocs.cloud/applications) page.
3. Create the `samples` storage for exchanging files by clicking the _plus_ icon and following the required steps. _Internal storage_ with _24-hour_ retention will suffice.
4. Provide the application name, for example, _HelloWorld_.
5. Click **Save** button.
6. Click the newly created **HelloWorld** application and copy the values from **Client Id** and **Client Secret** fields.

Now request an access token with the following API call:

```bash
curl --location --request POST 'https://id.groupdocs.cloud/connect/token' \
     --data-urlencode 'grant_type=client_credentials' \
     --data-urlencode 'client_id=CLIENT-ID-VALUE' \
     --data-urlencode 'client_secret=CLIENT-SECRET-VALUE'
```

You should get a response that looks something like this:

```json
{
	"access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...J5xlBi7mQfuNMzxpjUGVCUOOuGEd6iuJCbMaGanlhA9g",
	"expires_in": 3600,
	"token_type": "Bearer"
}
```

{{% alert color="primary" %}} 
The access token will be valid for the number of seconds specified in the `expires_in` property. If it has expired, request a new one using the same credentials.
{{% /alert %}} 

## Sending text for translation

Let's translate the following simple text from English to German:

```
Hello, world! I can read this text in my language.
```

The translation is carried out in 2 stages. First we need to POST a request to the GroupDocs.Translation Cloud API with parameters in JSON format in the body:

```bash
curl --location --request POST 'https://api.groupdocs.cloud/v2.0/translation/text' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...J5xlBi7mQfuNMzxpjUGVCUOOuGEd6iuJCbMaGanlhA9g' \
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

The authorization header must contain the access token obtained [earlier](#getting-an-access-token).

Wait a moment. The request will be placed in the queue and you will get its unique identifier. For example:

```json
{
	"status": 202,
	"message": "Starting translation",
	"id": "cb87bd7c-4660-3033-88c7-2b30edb44a4d"
}
```

## Getting translated text

The translation will take a second or two, depending on the length of the text and the current GroupDocs.Translation Cloud load. After the translation is completed, the translated text can be obtained by sending the unique identifier of the request obtained on the previous step to `https://api.groupdocs.cloud/v2.0/translation/text/` endpoint:

```bash
curl --location 'https://api.groupdocs.cloud/v2.0/translation/text/cb87bd7c-4660-4044-88c7-2b30edb44a4d' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...J5xlBi7mQfuNMzxpjUGVCUOOuGEd6iuJCbMaGanlhA9g' \
```

The authorization header must contain the access token obtained [earlier](#getting-an-access-token).

You will get the following response:

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

## What’s next?

Congratulations! You have successfully translated the text using GroupDocs.Translation Cloud API.


Read the [Developer's Guide](/translation/developer-guide/) and [API Reference](https://api.groupdocs.cloud/v2.0/translation/swagger/index.html) for details on creating advanced translation solutions with GroupDocs.Translation Cloud.
