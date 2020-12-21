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


#### Get Client Id and Client Secret ####

Before you can make any requests to GroupDocs Cloud API you need to get Client Id and Client Secret.\
This will be used to invoke the GroupDocs Cloud API.

You can get it from any existing Application or you can create a new Application.\
For further details see [Create New Application and Get Client Id and Client Secret]({{< ref "total/getting-started/ui-topics/creating-and-managing-application.md" >}})


#### Get your JWT token ####

After you have created a new application you can obtain a JWT token. See [this page]({{< ref "total/getting-started/overview-rest-api/authenticating-api-requests.md" >}}) for further details about this.


#### Call Rest API ####

When you’ve got your access_token you can make Rest API call by adding to Headers of your request:

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

{{< tabs tabTotal="3" tabID="1" tabName1="C#" tabName2="Java" tabName3="Python" >}} {{< tab tabNum="1" >}}

{{< gist groupdocscloud ffdd7c22bdf290769f6aa83bb870a80d Translation_CSharp_Translate_Text.cs >}}

{{< /tab >}} {{< tab tabNum="3" >}}

{{< gist groupdocscloud a8f3182d5ec6edb3b9dbc847acd5c097 translation_python_translate_text.py >}}

{{< /tab >}} {{< tab tabNum="2" >}}

{{< gist groupdocscloud 6ba7a98f4edadec75f6e8eac52d2885e Translation_Java_Translate_Text.java >}}

{{< /tab >}} {{< /tabs >}}

##### To translate document #####

###### cURL ######

Request

``` 
curl -X POST "https://api.groupdocs.cloud/v1.0/translation/document" \
-H "Authorization: Bearer TOKEN" \
-H "Content-Type: application/json" \
-d "'[ { \"format\":\"docx\", \"outformat\":\"docx\", \"pair\":\"en-fr\", \"name\":\"document.docx\", \"folder\":\"myFolder\", \"savepath\":\"myFolder\", \"savefile\":\"translatedDoc.docx\", \"storage\":\"MyStorage\", \"masters\": false, \"elements\": []}]'"
```

Response

``` 
{
    "status": "ok",
    "message": ".docx file saved successfully"
}
```

###### SDKs ######

{{< tabs tabTotal="3" tabID="1" tabName1="C#" tabName2="Java" tabName3="Python" >}} {{< tab tabNum="1" >}}

{{< gist groupdocscloud ffdd7c22bdf290769f6aa83bb870a80d Translation_CSharp_Translate_Document.cs >}}

{{< /tab >}} {{< tab tabNum="3" >}}

{{< gist groupdocscloud a8f3182d5ec6edb3b9dbc847acd5c097 translation_python_translate_document.py >}}

{{< /tab >}} {{< tab tabNum="2" >}}

{{< gist groupdocscloud 6ba7a98f4edadec75f6e8eac52d2885e Translation_Java_Translate_Document.java >}}

{{< /tab >}} {{< /tabs >}}


