---
id: "text-sdk"
weight: 30
date: "2023-11-01"
author: "Vladimir Lapin"
type: docs
url: translation/text/sdk/
productName: "GroupDocs.Translation Cloud"
title: Translating text with GroupDocs.Translation SDK
description: How to use GroupDocs.Translation Cloud SDK for translating texts.
keywords:
- translate
- API
- porogram
- language
- text
- content
---

Although you can directly call the GroupDocs.Translation Cloud REST API to [send text for translation](/translation/text/request/) and [fetch translated text](/translation/text/fetch/), there is a much easier way to implement translation functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with GroupDocs.Translation Cloud services much easier, allowing you to focus on business logic rather than technical details. Keep in mind, that for usage in non trial mode, you should get your [CliendId and ClientSecret](/translation/authorization/)

{{< tabs "example1" >}}

{{< tab ".NET (C#)" >}}

```csharp
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Threading;
using GroupDocs.Translation.Cloud.Sdk.Api;
using GroupDocs.Translation.Cloud.Sdk.Client;
using GroupDocs.Translation.Cloud.Sdk.Client.Auth;
using GroupDocs.Translation.Cloud.Sdk.Extensions;
using GroupDocs.Translation.Cloud.Sdk.Model;
using HttpStatusCode = System.Net.HttpStatusCode;

namespace GroupDocs.Translation.Cloud.Sdk
{
	public class TextTranslator
	{
		public TextTranslator()
		{
			Configuration config = new Configuration();
			/** Authorize your requests to GroupDocs.Translation Cloud */
			config.OAuthFlow = OAuthFlow.APPLICATION;
			config.OAuthClientId = "YOU_CLIENT_ID";
			config.OAuthClientSecret = "YOU_CLIENT_SECRET";
			/** Initialize GroupDocs.Translation API */
			config.BasePath = "https://api.groupdocs.cloud/v2.0/translation";
			TranslationApi apiInstance = new TranslationApi(config);
			/** Specify translation parameters */
			List<string> translateFrom = new List<string>() { "Hello, world! I can read this text in my language." };
			string sourceLanguage = "en";
			var targetLanguages = new List<string>() { "de" };
			var request = new TextRequest(
				sourceLanguage: sourceLanguage,
				targetLanguages: targetLanguages, 
				texts: translateFrom);
			/** Send text to translation */
			StatusResponse translationStatus = apiInstance.TextPost(request);
			/** Wait for results from translation queue */
			if(translationStatus.Status.ToSystemHttpStatusCode() == HttpStatusCode.Accepted)
			{
				while(true)
				{
					var result = apiInstance.TextRequestIdGet(translationStatus.Id);
					if(result.Status.ToSystemHttpStatusCode() == HttpStatusCode.OK)
					{
						Console.WriteLine(result.Translations[targetLanguages].First());
						break;
					}
					Thread.Sleep(1000);
				}
			}
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-dotnet
{{< /tab >}}
{{< tab "Python" >}}

```python
import time

import groupdocs_translation_cloud
from groupdocs_translation_cloud import TextRequest, Format

api = groupdocs_translation_cloud.api.TranslationApi()
api.api_client.configuration.client_id = "YOU_CLIENT_ID"
api.api_client.configuration.client_secret = "YOU_CLIENT_SECRET"

text_request = TextRequest(source_language="en"
                           , target_languages=["es", "fr", "ru"]
                           , texts=["Hello World!", "This is a test text"]
                           , origin="your_application_name"
                           , contains_markdown=False)
response = api.text_post(text_request)
if response.status == 202:
    while True:
        status_response = api.text_request_id_get(response.id)
        if status_response.status == 200:
            for lang in status_response.translations:
                print(lang + ": " + status_response.translations[lang][0])
            break
        time.sleep(2)
```

Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-python
{{< /tab >}}
{{< tab "Java & Android" >}}

```java
package com.groupdocs;
// Import classes:

import com.groupdocs.model.*;
import org.openapitools.client.api.TranslationApi;

public class TextDemo {
    public static void main(String[] args) {
        String basePath = "https://api.groupdocs.cloud/v2.0/translation";
        String cliendId = "YOUR_CLIENT_ID";
        String clientSecret = "YOUR_CLIENT_SECRET";

        ApiClient defaultClient = new ApiClient(basePath, cliendId, clientSecret, null);
        TranslationApi translationApi = new TranslationApi(defaultClient);

        TextRequest request = new TextRequest();

        request.setSourceLanguage("en");
        request.addTargetLanguagesItem("de");
        request.addTextsItem("Text to translate");
        request.setOrigin("");
        
        try {
            String r = translationApi.textPost(request).getId();
            CloudTextResponse response = translationApi.textRequestIdGet(r);
            if (!response.getStatus().toString().equals("500")) {
                while (true) {
                    response = translationApi.textRequestIdGet(r);
                    if (response.getStatus().toString().equals("200")) {
                        System.out.println(response);
                        break;

                    }
                    try {
                        Thread.sleep(2000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                }
            }
        }
        catch(ApiException e){
            System.err.println("Exception when calling TranslationApi#textPost");
            System.err.println("Status code: " + e.getCode());
            System.err.println("Reason: " + e.getResponseBody());
            System.err.println("Response headers: " + e.getResponseHeaders());
            e.printStackTrace();
        }
    }
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-java
{{< /tab >}}

{{< /tabs >}}
