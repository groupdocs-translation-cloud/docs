---
id: "quickstart"
url: "translation/quickstart"
title: "Quickstart"
productName: "GroupDocs.Translation Cloud"
weight: 4
description: ""
keywords: ""
---

####   ####

#### Create an account ####

Creating an account is very simple. Go to [https://dashboard.groupdocs.cloud](https://dashboard.groupdocs.cloud) to create a free account.


#### Get App Key and SID ####

Before you can make any requests to GroupDocs Cloud API you need to get APP SID and APP key (secret key). This will be used to invoke the GroupDocs Cloud API.

You can get it from the default Application or create a new Application. For further details see [Create New App and Get App Key and SID>>doc:translationcloud.getting-started.create-new-app-and-get-app-key-and-sid.WebHome)


#### Get your JWT token ####

After you have created a new application you can obtain a JWT token. See [JSON Web Token Authentication>>doc:translationcloud.getting-started.json-web-token-authentication.WebHome) for further details.


#### Call Rest API ####

When you’ve got your access_token your can make Rest API call by adding to Headers of your request:

* Authorization: Bearer access_token

##### To translate plain text #####

###### cURL ######

Request

```
curl -X POST "https://api.groupdocs.cloud/v1.0/translation/text" \
-H "Authorization: Bearer TOKEN" \
-H "Content-Type: application/json" \
-d "'[{\"pair\": \"en-fr\", \"text\": \"Welcome to Paris\"}]'"
```

Response

``` 
{
    "status": "ok",
    "message": "Text translated successfully",
    "translation": "Bienvenue à Paris"
}
```



###### SDKs ######

C#

{{< gist groupdocscloud ffdd7c22bdf290769f6aa83bb870a80d Translation_CSharp_Translate_Text.cs >}}

Python

{{< gist groupdocscloud a8f3182d5ec6edb3b9dbc847acd5c097 translation_python_translate_text.py >}}

Java

{{< gist groupdocscloud 6ba7a98f4edadec75f6e8eac52d2885e Translation_Java_Translate_Text.java >}}


##### To translate document #####

###### cURL ######

Request

``` 
curl -X POST "https://api.groupdocs.cloud/v1.0/translation/document" \
-H "Authorization: Bearer TOKEN" \
-H "Content-Type: application/json" \
-d "'[ { \"format\":\"docx\", \"pair\":\"en-fr\", \"name\":\"document.docx\", \"folder\":\"myFolder\", \"savepath\":\"myFolder\", \"savefile\":\"translatedDoc.docx\", \"storage\":\"MyStorage\" }]'"
```

Response

``` 
{
    "status": "ok",
    "message": "word file saved successfully"
}
```

###### SDKs ######

C#

{{< gist groupdocscloud ffdd7c22bdf290769f6aa83bb870a80d Translation_CSharp_Translate_Document.cs >}}

Python

{{< gist groupdocscloud a8f3182d5ec6edb3b9dbc847acd5c097 translation_python_translate_document.py >}}

Java

{{< gist groupdocscloud 6ba7a98f4edadec75f6e8eac52d2885e Translation_Java_Translate_Document.java >}}




