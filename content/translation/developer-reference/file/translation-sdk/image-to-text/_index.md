---
id: "image-to-text-sdk"
weight: 50
date: "2023-11-01"
author: "Vladimir Lapin"
type: docs
url: /translation/file/sdk/image-to-text/
productName: "GroupDocs.Translation Cloud"
title: Translating image files with GroupDocs.Translation SDK
description: How to use GroupDocs.Translation Cloud SDK for translating image files.
keywords:
- translate
- API
- porogram
- language
- text
- file
- content
---

Although you can directly call the GroupDocs.Translation Cloud REST API to [send image file for translation](/translation/file/request/image-to-text/) and [fetch translated file](/translation/file/fetch/), there is a much easier way to implement translation functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with GroupDocs.Translation Cloud services much easier, allowing you to focus on business logic rather than technical details.

{{< tabs tabID="1" tabTotal="3" tabName1=".NET (C#)" tabName2="Python" tabName3="Java" >}}
{{< tab tabNum="1" >}}

```csharp
using System.IO;
using System.Collections.Generic;
using System.Net.Http;
using GroupDocs.Translation.Cloud.Sdk.Api;
using GroupDocs.Translation.Cloud.Sdk.Client;
using GroupDocs.Translation.Cloud.Sdk.Client.Auth;
using GroupDocs.Translation.Cloud.Sdk.Model;
using Configuration = GroupDocs.Translation.Cloud.Sdk.Client.Configuration;
using HttpStatusCode = System.Net.HttpStatusCode;

namespace GroupDocs.Translation.Cloud.Sdk
{
	public class FileTranslator
	{
		public FileTranslator()
		{
			Configuration config = new Configuration();
			/** Authorize your requests to GroupDocs.Translation Cloud */
			config.OAuthFlow = OAuthFlow.APPLICATION;
			config.OAuthClientId = "YOU_CLIENT_ID";
			config.OAuthClientSecret = "YOU_CLIENT_SECRET";
			/** Initialize GroupDocs.Translation API */
			config.BasePath = "https://api.groupdocs.cloud/v2.0/translation";
			TranslationApi api = new TranslationApi(config);
			FileApi fileApi = new FileApi(config);
			/** Specify translation parameters */
			string filePath = "/path/to/myfile.pdf";
			string savePath = "/path/to/savefile/";
			string sourceLanguage = "en";
			var targetLanguages = new List<string>() { "de" };
			string format = "pdf";
			byte[] file = File.ReadAllBytes(filePath);
			MemoryStream ms = new MemoryStream(file);
			string url = fileApi.FileUploadPost(format, ms);
			CloudTextResponse response = new CloudTextResponse();
			var request = new ImageToTextRequest(
				sourceLanguage: sourceLanguage,
				targetLanguages: targets,
				url: url,
				format: ImageToTextRequest.FormatEnum.Pdf);
			/** Send file to translation */
			var responseId = await api.ImageToTextPostAsync(request);			
			/** Wait for results from translation queue */
			try
			{
				if ((HttpStatusCode)responseId.Status == HttpStatusCode.Accepted)
				{
					while (true)
					{
						response = await api.TextRequestIdGetAsync(responseId.Id);
						if (response.Translations.Count > 0)
							foreach (string lang in targets)
							{
								for (int i = 0; i < response.Translations[lang].Count; i++)
								{
									Console.WriteLine($"Image {lang}-{i} translation: {response.Translations[lang][i]}");
								}
							}
							break;
						else
							Thread.Sleep(2000);
					}
				}
				else
				{
					response = new CloudTextResponse() { Status = responseId.Status, Message = responseId.Message };
					Console.WriteLine("error: " + response.Message);
				}
			}
			catch (Exception ex)
			{
				Console.WriteLine("exception: " + ex.ToString());
			}    
		}
	}
}
```
Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-dotnet
{{< /tab >}}
{{< tab tabNum="2" >}}

```python
import time

import groupdocs_translation_cloud
from groupdocs_translation_cloud import ImageToTextRequest, Format

api = groupdocs_translation_cloud.api.TranslationApi()
file_api = groupdocs_translation_cloud.api.FileApi()
api.api_client.configuration.client_id = "YOU_CLIENT_ID"
api.api_client.configuration.client_secret = "YOU_CLIENT_SECRET"

url = file_api.file_upload_post(file="/path/to/yourfile.pdf", format=Format.Pdf)
file_request = ImageToTextRequest(source_language="en", 
							           target_languages=["ru"], 
							           url=url, 
							           format=Format.Pdf)
response = api.image_to_text_post(file_request)
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

{{< tab tabNum="3" >}}

```java
package com.groupdocs;
// Import classes:

import com.groupdocs.model.*;
import org.openapitools.client.api.TranslationApi;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class StrDemo {
    public static void main(String[] args) {
        String basePath = "https://api.groupdocs.cloud/v2.0/translation";
        String cliendId = "YOUR_CLIENT_ID";
        String clientSecret = "YOUR_CLIENT_SECRET";

        ApiClient defaultClient = new ApiClient(basePath, cliendId, clientSecret, null);
        TranslationApi translationApi = new TranslationApi(defaultClient);
        FileApi fileApi = new FileApi(defaultClient);

        ImageToTextRequest fileRequest = new ImageToTextRequest();

        String fileName = "FILE_PATH";
        File fileToTranslate = new File(fileName);
        String file_url = fileApi.fileUploadPost("FILE_FORMAT", fileToTranslate);        fileRequest.setSource("en");
        fileRequest.addTargetsItem("fr");
        fileRequest.setFormat(ImageToTextRequest.FormatEnum.JPG);
        fileRequest.setUrl(file_url);


        try {
            StatusResponse response = translationApi.imageToTextPost(fileRequest);
            String _id = response.getId();
            if (!response.getStatus().toString().equals("500")) {
                while (true) {
                    CloudTextResponse textResponse = translationApi.textRequestIdGet(_id);
                    if (textResponse.getStatus().toString().equals("200")){
                        System.out.println(textResponse);
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
            System.err.println("Exception when calling TranslationApi#imageToTextPost");
            System.err.println("Status code: " + e.getCode());
            System.err.println("Reason: " + e.getResponseBody());
            System.err.println("Response headers: " + e.getResponseHeaders());
            e.printStackTrace();
        }
        catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/groupdocs-translation-cloud/groupdocs-translation-cloud-java
{{< /tab >}}

{{< /tabs >}}