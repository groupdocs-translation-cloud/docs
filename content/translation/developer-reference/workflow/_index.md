---
id: "workflow"
weight: 10
date: "2023-10-17"
author: "Vladimir Lapin"
type: docs
url: /translation/workflow/
aliases:
- /translation/introduction/
productName: "GroupDocs.Translation Cloud"
title: Translation workflow
description: An overview of the GroupDocs.Translation Cloud workflow.
keywords:
- flow
- process
- steps
- diagram
- process
- request
- response
toc: True
---

GroupDocs.Translation Cloud can translate texts and and documents in a [number of formats](/translation/supported-file-formats/) with just 2 REST API calls or a few lines of code in any programming language supported by [SDK](/translation/sdk/). Read [Hello, world!](/translation/hello-world/) article for a hands-on example.

![GroupDocs.Translation Cloud workflow](/translation/workflow/groupdocs-cloud-flow.png)

## 1. Send text or file for translation

In the request body, provide JSON with a plain text, a _Base64_ encoded file, or a URL to translate, along with mandatory and optional translation parameters.

To authorize the request to use GroupDocs.Translation Cloud, pass the [access token](/translation/authorization/) in _Authorization_ header of the request (_Bearer Token_).

{{% alert color="primary" %}} 
If you are using [GroupDocs.Translation Cloud SDK](/translation/sdk/), you do not have to worry about content encoding, getting an access token, setting request headers, and other technical details. The SDK will perform all routine operations: from establishing a connection with the GroupDocs.Translation Cloud API to receiving and parsing the response.
{{% /alert %}} 

## 2. Get the request ID

Your translation request is queued and you will receive a unique identifier that can be used to retrieve results.

For more information on what happens in the cloud, read [Behind the scenes](#behind-the-scenes) section.

## 3. Fetch the translation

Just call the GroupDocs.Translation Cloud API with the ID of the request received on the previous step to retrieve the translation. The translation may take a second or two, depending on the file size and complexity and the current GroupDocs.Translation load. For more information on what happens in the cloud, read [Behind the scenes](#behind-the-scenes) section.

To authorize your request, pass the [access token](/translation/authorization/) in _Authorization_ header.

{{% alert color="primary" %}} 
If you are using [GroupDocs.Translation Cloud SDK](/translation/available-sdks/), it will handle all authorization routines.
{{% /alert %}} 

## 4. Working with the translation

If the translation is successful, you will receive the results in JSON format along with processing statistics. Translated files are returned as URLs which can be downloaded, displayed on the screen, or written to a database. Translated text is returned as an array of strings.

{{% alert color="primary" %}}
[GroupDocs.Translation Cloud SDK](/translation/available-sdks/) takes care of all the routine operations so you can get content directly with no extra effort.
{{% /alert %}}

## Behind the scenes

Machine translation is a resource-intensive process that involves sophisticated neural networks and complex calculations. Even with high-performance servers, this can take some time, especially when translating large amounts of content and reading large files.

To balance resources under high load and ensure reliable and secure operation, we have introduced _queued processing_. Instead of being immediately sent for translation, the source image text or file is placed in a queue under a unique identifier. The queue is constantly monitored and processed in the background using advanced load balancing techniques.

Once the translation is ready, the result is saved to internal storage, from where it can be retrieved using the unique ID within **24 hours** after a translation request has been made.
