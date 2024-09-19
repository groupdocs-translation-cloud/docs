---
id: "sdk"
weight: 50
date: "2022-06-17"
author: "Vladimir Lapin"
type: docs
url: translation/sdk
productName: "GroupDocs.Translation Cloud"
title: Available SDKs
description: Find the latest software development kits (SDKs) that help you easily integrate GroupDocs.Translation Cloud into your applications.
keywords:
- .NET
- Java
- Python
- Android
- programming
- SDK
---

GroupDocs offers software development kits (SDKs) for popular programming languages that make interaction with GroupDocs.Translation cloud services much easier. It allows you to focus on business logic rather than the technical details.

SDKs handle all the routine operations such as establishing connections, sending API requests, and parsing responses, wrapping all these tasks into a few simple methods. The following programming languages are supported:

- [GroupDocs.Translation Cloud for .NET](https://products.groupdocs.cloud/translation/net)  
  Use the translation features in any on-premise and web-based .NET application.
- [GroupDocs.Translation Cloud for Python](https://products.groupdocs.cloud/translation/python)  
  Natively integrate translation features into data analytics, finance, AI, and other Python applications.
- [GroupDocs.Translation Cloud for Java](https://products.groupdocs.cloud/translation/java)  
  Use GroupDocs.Translation in cross-platform Java apps.
- [GroupDocs.Translation Cloud for Android](https://products.groupdocs.cloud/translation/android)  
  Extend your mobile apps with translation features. GroupDocs.Translation service runs in the cloud and supports even entry-level and legacy smartphones.

All SDKs are open-source distributed under [MIT License](https://opensource.org/licenses/MIT). You can freely use them for any projects, including commercial and proprietary applications, as well as modify any part of the code.

The provided code is fully tested and ready to run out of the box.

## SDK usage examples

See the examples below for a quick overview of how SDKs can make your development easier.

### Translating the text 

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
			string translateFrom = new List<string>() { "Hello, world! I can read this text in my language." };
			string sourceLanguage = "en";
			var targetLanguages = new List<string>() { "de" };
			var request = new TextRequest(sourceLanguage, targetLanguages, translateFrom, origin: "demo");
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

Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-dotnet
{{< /tab >}}
{{< /tabs >}}
