---
id: "text-sdk"
weight: 30
date: "2023-11-01"
author: "Vladimir Lapin"
type: docs
url: /translation/text/sdk/
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

Although you can directly call the GroupDocs.Translation Cloud REST API to [send text for translation](/translation/text/request/) and [fetch translated text](/translation/text/fetch/), there is a much easier way to implement translation functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with GroupDocs.Translation Cloud services much easier, allowing you to focus on business logic rather than technical details.

{{< tabs "example1">}}
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
            string translateFrom = new List<string>() { "Hello, world! I can read this text in my             language." };
            string sourceLanguage = "en";
            var targetLanguages = new List<string>() { "de" };
            var request = new TextRequest(sourceLanguage, targetLanguages, translateFrom, origin:             "demo");
            /** Send text to translation */
            StatusResponse translationStatus = apiInstance.TextPost(request);
            /** Wait for results from translation queue */
            if(translationStatus.Status.ToSystemHttpStatusCode() == HttpStatusCode.Accepted)
            {
                while(true)
                {
                    var result = apiInstance.TextRequestIdGet(statusResponse.Id);
                    if(result.Status.ToSystemHttpStatusCode() == HttpStatusCode.OK)
                    {
                        Console.WriteLine(result.Translations[toLang].First());
                        break;
                    }
                    Thread.Sleep(1000);
                }
            }
        }
    }
}
```
{{< /tab >}} {{< /tabs >}}

Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-dotnet
