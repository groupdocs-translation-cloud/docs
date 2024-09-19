---
id: "authorization"
weight: 20
date: "2023-10-19"
author: "Vladimir Lapin"
type: docs
url: translation/authorization/
productName: "GroupDocs.Translation Cloud"
title: Authorization
description: How to get an access token and use it to authorize GroupDocs.Translation Cloud API requests.
keywords:
- REST
- header
- auth
- access
- security
---

GroupDocs.Translation Cloud follows industry standards and best practices to keep your data secure. All communication with GroupDocs.Translation Cloud REST API is done using JWT authentication, which provides an open-standard, highly secure way to exchange information.

## Getting an access token

Time-limited JWT tokens are generated using _Client ID_ and _Client Secret_ credentials that are specific for each application. To obtain the credentials:

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.groupdocs.cloud/).
2. Go to [**Applications**](https://dashboard.groupdocs.cloud/applications) page.
3. Click **Create New Application** button.
4. Give the application an easily recognizable name so it can be quickly found in a long list, and provide an optional detailed description.
5. Create the cloud storage by clicking the _plus_ icon and following the required steps. You can also reuse existing storage, if available.   
   GroupDocs.Translation Cloud uses its own internal storage, so you can provide the bare minimum storage options:

    - Type: **Internal storage**
    - Storage name: _Any name you like_
    - Storage mode: **Retain files for 24 hours**

6. Click **Save** button.
7. Click the newly created application and copy the values from **Client Id** and **Client Secret** fields.

{{% alert color="primary" %}} 
Keep your credentials safe! If you feel that they might be compromised, regenerate them immediately.
{{% /alert %}}

Now request an access token by sending the **POST** request to `https://id.groupdocs.cloud/connect/token` with the following parameters in the request body (x-www-form-urlencoded):

- `grant_type` - must be `client_credentials`
- `client_id` - the value from **Client Id** field.
- `client_secret` - the value from **Client Secret** field.

{{< tabs "example1" >}}
{{< tab "Request" >}}
```bash
curl --location --request POST 'https://id.groupdocs.cloud/connect/token' \
     --header 'Content-Type: application/x-www-form-urlencoded' \
     --data-urlencode 'grant_type=client_credentials' \
     --data-urlencode 'client_id=CLIENT-ID-VALUE' \
     --data-urlencode 'client_secret=CLIENT-SECRET-VALUE'
```
{{< /tab >}}
{{< tab "Response" >}}
```json
{
	"access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...BUNNec2iRtStPW2Ywek4iJmYwMbWONQ",
	"expires_in": 3600,
	"token_type": "Bearer"
}
```
{{< /tab >}}
{{< /tabs >}}

The access token is returned in `access_token` property of the response JSON and will be valid for the number of seconds specified in the `expires_in` property of the response JSON. If it has expired, request a new one using the same API call.

## Authorizing REST API requests

To authorize your requests to GroupDocs.Translation Cloud API, pass the access token in **Authorization** header of each request (_Bearer authentication_):

```bash
curl --location --request POST 'https://api.groupdocs.cloud/v2.0/translation/text' \
     --header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...J5xlBi7mQfuNMzxpjUGVCUOOuGEd6iuJCbMaGanlhA9g'
```

## Authorizing SDK requests

The SDKs greatly simplify all operations for obtaining an access token and authorizing requests. Just pass in the values from the **Client ID** and **Client Secret** fields when initializing the translation API and it will do the rest for you.

{{< tabs "example2" >}}

{{< tab ".NET (C#)" >}}
```csharp
Configuration config = new Configuration();
/** Authorize your requests to GroupDocs.Translation Cloud */
config.OAuthFlow = OAuthFlow.APPLICATION;
config.OAuthClientId = "YOU_CLIENT_ID";
config.OAuthClientSecret = "YOU_CLIENT_SECRET";
/** Initialize GroupDocs.Translation API */
config.BasePath = "https://api.groupdocs.cloud/v2.0/translation";
TranslationApi apiInstance = new TranslationApi(config);
```

Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-dotnet
{{< /tab >}}
{{< tab "Python" >}}
```python
import groupdocs_translation_cloud
# Initialize GroupDocs.Translation API
api = groupdocs_translation_cloud.api.TranslationApi()
# Authorize your requests to GroupDocs.Translation Cloud 
api.api_client.configuration.client_id = "YOU_CLIENT_ID"
api.api_client.configuration.client_secret = "YOU_CLIENT_SECRET"
```

Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-python
{{< /tab >}}
{{< tab "Java & Android" >}}
```java
// Authorize your requests to GroupDocs.Translation Cloud
String basePath = "https://api.groupdocs.cloud/v2.0/translation";
String cliendId = "YOUR_CLIENT_ID";
String clientSecret = "YOUR_CLIENT_SECRET"; 
// Initialize GroupDocs.Translation API
ApiClient defaultClient = new ApiClient(basePath, cliendId, clientSecret, null);
TranslationApi translationApi = new TranslationApi(defaultClient);
```

Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-java
{{< /tab >}}

{{< /tabs >}}
