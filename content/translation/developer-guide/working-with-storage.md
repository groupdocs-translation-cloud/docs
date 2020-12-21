---
id: "working-with-storage"
url: "translation/working-with-storage"
title: "Working With Storage"
productName: "GroupDocs.Translation Cloud"
weight: 8
description: ""
keywords: ""
---

 





# Storage existence API #

This API intended for checking the existence of cloud storage with a given name from [GroupDocs Cloud Storage](https://dashboard.groupdocs.cloud).

## API Explorer ##

[GroupDocs.Translation Cloud API Reference](https://apireference.groupdocs.cloud/translation/#/) lets you try out [Storage existence API](https://apireference.groupdocs.cloud/translation/#/Storage/StorageExists) right away in your browser! It allows you to effortlessly interact and try out every single operation our APIs expose.

### Request parameters ###

|**Parameter**|**Description**|
|---|---|
|**storageName**|Storage name|

## cURL Example ##

Request

``` 
curl -X GET "https://api.groupdocs.cloud/v1.0/translation/storage/MyStorage/exist" -H  "accept: application/json" -H  "authorization: Bearer  [Access Token]"
```
Response

``` 
{
  "exists": true
}
```

## SDKs ##

Our API is completely independent of your operating system, database system or development language. You can use any language and platform that supports HTTP to interact with our API. However, manually writing client code can be difficult, error-prone and time-consuming. Therefore, we have provided and support API [SDKs](https://github.com/groupdocs-translation-cloud) in many development languages in order to make it easier to integrate with us. If you use [SDK](https://github.com/groupdocs-translation-cloud), it hides the [File API](https://apireference.groupdocs.cloud/translation/#/File) calls and lets you use GroupDocs Cloud features in a native way for your preferred language.

### SDK Examples ###

{{< tabs tabTotal="3" tabID="1" tabName1="C#" tabName2="Java" tabName3="Python" >}} {{< tab tabNum="1" >}}

{{< gist groupdocscloud ffdd7c22bdf290769f6aa83bb870a80d Translation_CSharp_Storage_Exists.cs >}}

{{< /tab >}} {{< tab tabNum="3" >}}

{{< gist groupdocscloud a8f3182d5ec6edb3b9dbc847acd5c097 translation_python_storage_exists.py >}}

{{< /tab >}} {{< tab tabNum="2" >}}

{{< gist groupdocscloud 6ba7a98f4edadec75f6e8eac52d2885e Translation_Java_Storage_Exists.java >}}

{{< /tab >}} {{< /tabs >}}

# Storage object existence API #

This API intended for checking the existence of a file or folder in [GroupDocs Cloud Storage](https://dashboard.groupdocs.cloud).

## API Explorer ##

[GroupDocs.Translation Cloud API Reference](https://apireference.groupdocs.cloud/translation/#/) lets you try out [Storage existence API](https://apireference.groupdocs.cloud/translation/#/Storage/StorageExists) right away in your browser! It allows you to effortlessly interact and try out every single operation our APIs expose.

### Request parameters ###

|**Parameter**|**Description**|
|---|---|
|**path**|Path of the file or folder<br>Required. Can be passed as a query string parameter or as part of the URL|
|storageName|Name of the storage. If not set, then default storage used|
|versionId|File version id|

## cURL Example ##

Request

``` 
curl -X GET "https://api.groupdocs.cloud/v1.0/translation/storage/exist/editordocs?storageName#MyStorage" -H  "accept: application/json" -H  "authorization: Bearer [Access Token]"
```

Response

``` 
{
  "exists": true,
  "isFolder": true
}
```

## SDKs ##

Our API is completely independent of your operating system, database system or development language. You can use any language and platform that supports HTTP to interact with our API. However, manually writing client code can be difficult, error-prone and time-consuming. Therefore, we have provided and support API [SDKs](https://github.com/groupdocs-translation-cloud) in many development languages in order to make it easier to integrate with us. If you use [SDK](https://github.com/groupdocs-translation-cloud), it hides the [File API](https://apireference.groupdocs.cloud/translation/#/File) calls and lets you use GroupDocs Cloud features in a native way for your preferred language.

### SDK Examples ###

{{< tabs tabTotal="3" tabID="1" tabName1="C#" tabName2="Java" tabName3="Python" >}} {{< tab tabNum="1" >}}

{{< gist groupdocscloud ffdd7c22bdf290769f6aa83bb870a80d Translation_CSharp_Object_Exists.cs >}}

{{< /tab >}} {{< tab tabNum="3" >}}

{{< gist groupdocscloud a8f3182d5ec6edb3b9dbc847acd5c097 translation_python_object_exists.py >}}

{{< /tab >}} {{< tab tabNum="2" >}}

{{< gist groupdocscloud 6ba7a98f4edadec75f6e8eac52d2885e Translation_Java_Object_Exists.java >}}

{{< /tab >}} {{< /tabs >}}

# Storage Space Usage API #

This API intended for getting total and used space of the[ GroupDocs Cloud Storage](https://dashboard.groupdocs.cloud)

## API Explorer ##

[GroupDocs.Translation Cloud API Reference](https://apireference.groupdocs.cloud/translation/#/) lets you try out [storage space usage API](https://apireference.groupdocs.cloud/translation/#/Storage/GetDiscUsage) right away in your browser! It allows you to effortlessly interact and try out every single operation our APIs expose.

### Request parameters ###

|**Parameter**|**Description**|
|---|---|
|storageName|Name of the storage. If not set, then default storage used|

## cURL Example ##

Request

``` 
curl -X GET "https://api.groupdocs.cloud/v1.0/translation/storage/disc?storageName#MyStorage" -H  "accept: application/json" -H  "authorization: Bearer [Access Token]"
```

Response

``` 
{
  "usedSize": 31032368,
  "totalSize": 3221225472
}
```

## SDKs ##

Our API is completely independent of your operating system, database system or development language. You can use any language and platform that supports HTTP to interact with our API. However, manually writing client code can be difficult, error-prone and time-consuming. Therefore, we have provided and support API [SDKs](https://github.com/groupdocs-translation-cloud) in many development languages in order to make it easier to integrate with us. If you use [SDK](https://github.com/groupdocs-translation-cloud), it hides the [File API](https://apireference.groupdocs.cloud/translation/#/File) calls and lets you use GroupDocs Cloud features in a native way for your preferred language.

### SDK Examples ###

{{< tabs tabTotal="3" tabID="1" tabName1="C#" tabName2="Java" tabName3="Python" >}} {{< tab tabNum="1" >}}

{{< gist groupdocscloud ffdd7c22bdf290769f6aa83bb870a80d Translation_CSharp_Space_Usage.cs >}}

{{< /tab >}} {{< tab tabNum="3" >}}

{{< gist groupdocscloud a8f3182d5ec6edb3b9dbc847acd5c097 translation_python_space_usage.py >}}

{{< /tab >}} {{< tab tabNum="2" >}}

{{< gist groupdocscloud 6ba7a98f4edadec75f6e8eac52d2885e Translation_Java_Space_Usage.java >}}

{{< /tab >}} {{< /tabs >}}

# Storage File Versions API #

This API intended for getting the list of file versions, stored in the [GroupDocs Cloud Storage](https://dashboard.groupdocs.cloud)

## API Explorer ##

[GroupDocs.Translation Cloud API Reference](https://apireference.groupdocs.cloud/translation/#/) lets you try out [Storage File Versions API](https://apireference.groupdocs.cloud/translation/#/Storage/GetFileVersions) right away in your browser! It allows you to effortlessly interact and try out every single operation our APIs expose.

### Request parameters ###

|**Parameter**|**Description**|
|---|---|
|**path**|Path of the file including file name and extension e.g. /Folder1/file.ext<br>Required. Can be passed as a query string parameter or as part of the URL|
|storageName|Name of the storage. If not set, then default storage used|

## cURL Example ##

Request

``` 
curl -X GET "https://api.groupdocs.cloud/v1.0/translation/storage/version/one-page.docx?storageName#MyStorage" -H  "accept: application/json" -H  "authorization: Bearer [Access Token]"
```

Response

``` 
{
  "value": [
    {
      "versionId": "null",
      "isLatest": true,
      "name": "one-page.docx",
      "isFolder": false,
      "modifiedDate": "2018-08-16T19:45:05+00:00",
      "size": 347612,
      "path": "/one-page.docx"
    }
  ]
}
```

## SDKs ##

Our API is completely independent of your operating system, database system or development language. You can use any language and platform that supports HTTP to interact with our API. However, manually writing client code can be difficult, error-prone and time-consuming. Therefore, we have provided and support API [SDKs](https://github.com/groupdocs-translation-cloud) in many development languages in order to make it easier to integrate with us. If you use [SDK](https://github.com/groupdocs-translation-cloud), it hides the [File API](https://apireference.groupdocs.cloud/translation/#/File) calls and lets you use GroupDocs Cloud features in a native way for your preferred language.

### SDK Examples ###

{{< tabs tabTotal="3" tabID="1" tabName1="C#" tabName2="Java" tabName3="Python" >}} {{< tab tabNum="1" >}}

{{< gist groupdocscloud ffdd7c22bdf290769f6aa83bb870a80d Translation_CSharp_File_Versions.cs >}}

{{< /tab >}} {{< tab tabNum="3" >}}

{{< gist groupdocscloud a8f3182d5ec6edb3b9dbc847acd5c097 translation_python_file_versions.py >}}

{{< /tab >}} {{< tab tabNum="2" >}}

{{< gist groupdocscloud 6ba7a98f4edadec75f6e8eac52d2885e Translation_Java_File_Versions.java >}}

{{< /tab >}} {{< /tabs >}}
