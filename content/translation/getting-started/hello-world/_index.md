---
id: "hello-world"
weight: 40
date: "2022-06-17"
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

In this article, you will learn how to translate a simple Microsoft Word document from English to German using GroupDocs.Translation Cloud REST API.

{{% alert color="primary" %}} 

We assume that you have already [signed up](/translation/sign-up/) to the service and have not yet exceeded your [free subscription plan](/translation/subscription/) limits.

{{% /alert %}} 

## You will need

- [Any system](/translation/system-requirements/) with Internet connection.
- Microsoft Word. If you do not have Microsoft Office, you can try a different [file format](/translation/supported-file-formats/).
- A web browser.
- Any tool that allows you to make REST API calls, such as [cURL](https://curl.se/) or [Postman](https://www.postman.com/). The article provides cURL examples.
- **15 minutes** of spare time.

## Getting an access token

The GroupDocs.Translation Cloud API is fully compliant with industry security standards and best practices. Data transfer is carried out using JWT authentication, which eliminates all possibilities of data theft or disclosure.

To obtain a JWT token, get the _Client ID_ and _Client Secret_ credentials:

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.groupdocs.cloud/).
2. Go to [**Applications**](https://dashboard.groupdocs.cloud/applications) page.
3. Create the `samples` storage for exchanging files by clicking the _plus_ icon and following the required steps. For this example, _Internal storage_ with _24-hour_ retention will suffice.
4. Provide the application name, for example, _HelloWorld_.
5. Click **Save** button.
6. Click the newly created **HelloWorld** application and copy the values from **Client Id** and **Client Secret** fields.

Now request an access token with the following API call:

```bash
curl --location --request POST 'https://api.groupdocs.cloud/connect/token' \
     --header 'Content-Type: application/x-www-form-urlencoded' \
     --data-urlencode 'grant_type=client_credentials' \
     --data-urlencode 'client_id=CLIENT-ID-VALUE' \
     --data-urlencode 'client_secret=CLIENT-SECRET-VALUE'
```

You should get a response that looks something like this:

```json
{
	"access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...Iwr6g2zbFwf1nLtg",
	"expires_in": 3600,
	"token_type": "Bearer"
}
```

{{% alert color="primary" %}} 

The access token will be valid for the number of seconds specified in the `expires_in` property. If it has expired, request a new one using the same credentials.

{{% /alert %}} 

## Preparing a source file

Let's start with a simple document with minimal formatting:

![Source document](/translation/hello-world/source.png)

Save the document as `Hello.docx` in your `Documents` folder.

Now upload the file to the online storage, created on the previous step:

1. Open [**Files**](https://dashboard.groupdocs.cloud/files) page of **GroupDocs Cloud API Dashboard**.
2. Select `samples` storage.
3. Drag the `Hello.docx` from `Documents` folder to the storage.

## Translating

Now we are ready for the most intriguing part - the translation. Make the following API call:

```bash
curl --location --request POST 'https://api.groupdocs.cloud/v1.0/translation/document' \
     --header 'Content-Type: application/json' \
     --header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...Iwr6g2zbFwf1nLtg' \
     --data-raw ''\''[{\"format\":\"docx\", \"outformat\":\"docx\", \"pair\":\"en-de\", \"name\":\"Hello.docx\", \"savefile\":\"Hello-DE.docx\", \"storage\":\"samples\"}]'\'''
```

Read [JSON Request Details](/translation/json-request-details/) for more information on the request body parameters.

Wait a few seconds. You will get the following response:

```json
{
	"status": "ok",
	"message": ".docx file saved successfully, file was fully translated",
	"duration": 11.5256778,
	"details": null
}
```

### Getting the translated document

1. Open [**Files**](https://dashboard.groupdocs.cloud/files) page of **GroupDocs Cloud API Dashboard**.
2. Select `samples` storage.
3. Select `Hello-DE.docx` file and click **Download** in the toolbar.  
   If you do not see the file, click **Refresh** in the toolbar.
4. Open the downloaded document.

![Translated document](/translation/hello-world/target.png)

## What’s next?

Congratulations! You have taken the first step in neural machine translation. Read the [Developer's Guide](/translation/developer-guide/) and [API Reference](https://apireference.groupdocs.cloud/translation/) for details on creating advanced translation solutions with GroupDocs.Translation Cloud.
