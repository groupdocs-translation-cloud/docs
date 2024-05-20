---
id: "excel-sdk"
weight: 20
date: "2023-11-01"
author: "Vladimir Lapin"
type: docs
url: /translation/file/sdk/excel/
productName: "GroupDocs.Translation Cloud"
title: Translating Excel files with GroupDocs.Translation SDK
description: How to use GroupDocs.Translation Cloud SDK for translating Excel files.
keywords:
- translate
- API
- program
- language
- excel
- file
- content
---

Although you can directly call the GroupDocs.Translation Cloud REST API to [send Excel file for translation](/translation/file/request/excel/) and [fetch translated file](/translation/file/fetch/), there is a much easier way to implement translation functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with GroupDocs.Translation Cloud services much easier, allowing you to focus on business logic rather than technical details.

{{< tabs "example1" >}}
{{< tab ".NET (C#)" >}}

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
			string filePath = "/path/to/myfile.xlsx";
			string savePath = "/path/to/savefile/";
			string sourceLanguage = "en";
			var targetLanguages = new List<string>() { "de" };
			string format = "xlsx";
			string outputFormat = "xlsx";
			byte[] file = File.ReadAllBytes(filePath);
			MemoryStream ms = new MemoryStream(file);
			string url = fileApi.FileUploadPost(format, ms);
			CloudFileResponse response = new CloudFileResponse();
			var request = new SpreadsheetFileRequest(
				sourceLanguage: sourceLanguage,
				targetLanguages: targets,
				url: url,
				format: SpreadsheetFileRequest.FormatEnum.Xlsx,
				outputFormat: outputFormat,
				savingMode: SpreadsheetFileRequest.SavingModeEnum.Files);
			/** Send file to translation */
			var responseId = await api.SpreadsheetPostAsync(request);			
			/** Wait for results from translation queue */
			try
			{
				if ((HttpStatusCode)responseId.Status == HttpStatusCode.Accepted)
				{
					while (true)
					{
						response = await api.DocumentRequestIdGetAsync(responseId.Id);
						if (response.Urls.Count > 0)
							break;
						else
							Thread.Sleep(2000);
					}
					Console.WriteLine("File translated");
					using (var client = new HttpClient())
					{
						foreach (string lang in targets)
						{
							string savePath = $"{savepath}{lang}.{outputFormat}";    
							var result = await client.GetByteArrayAsync(response.Urls[lang].Url);                            File.WriteAllBytes(savePath, result);
						}
					}
				}
				else
				{
					response = new CloudFileResponse() { Status = responseId.Status, Message = responseId.Message };
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
{{< tab "Python" >}}

```python
import time

import groupdocs_translation_cloud
from groupdocs_translation_cloud import SpreadsheetFileRequest, Format

api = groupdocs_translation_cloud.api.TranslationApi()
file_api = groupdocs_translation_cloud.api.FileApi()
api.api_client.configuration.client_id = "YOU_CLIENT_ID"
api.api_client.configuration.client_secret = "YOU_CLIENT_SECRET"

url = file_api.file_upload_post(file="/path/to/yourfile.xlsx", format=Format.Xlsx)
file_request = SpreadsheetFileRequest(source_language="en", 
							           target_languages=["ru"], 
							           url=url, 
							           format=Format.Xlsx,
							           saving_mode=SavingMode.Files, 
							           output_format=Format.Xlsx)
response = api.spreadsheet_post(file_request)
if response.status == 202:
    while True:
        file_response = api.document_request_id_get(request_id)
        if file_response.status == 200:
            print(file_response.message)
            for lang in file_response.urls:
                print(lang + '_' + url + ': ' + file_response.urls[
                    lang].url)
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

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpredshhetDemo {
    public static void main(String[] args) {
        String basePath = "https://api.groupdocs.cloud/v2.0/translation";
        String cliendId = "YOUR_CLIENT_ID";
        String clientSecret = "YOUR_CLIENT_SECRET";

        ApiClient defaultClient = new ApiClient(basePath, cliendId, clientSecret, null);
        TranslationApi translationApi = new TranslationApi(defaultClient);
        FileApi fileApi = new FileApi(defaultClient);

        SpreadsheetFileRequest fileRequest = new SpreadsheetFileRequest();

        String fileName = "FILE_PATH";
        File fileToTranslate = new File(fileName);
        String file_url = fileApi.fileUploadPost("FILE_FORMAT", fileToTranslate);
        fileRequest.setSourceLanguage("ru");
        fileRequest.addTargetLanguagesItem("en");
        fileRequest.setFormat(SpreadsheetFileRequest.FormatEnum.XLSX);
        fileRequest.setOutputFormat(SpreadsheetFileRequest.OutputFormatEnum.XLSX);
        fileRequest.setSavingMode(SpreadsheetFileRequest.SavingModeEnum.FILES);
        fileRequest.setUrl(file_url);

        try {
            StatusResponse response = translationApi.spreadsheetPost(fileRequest);
            String _id = response.getId();
            if (!response.getStatus().toString().equals("500")) {
                while (true) {
                    CloudFileResponse fileResponse = translationApi.documentRequestIdGet(_id);
                    if (fileResponse.getStatus().toString().equals("200")){
                        System.out.println(fileResponse);
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
            System.err.println("Exception when calling TranslationApi#spreadsheetPost");
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