---
id: "json-request-details"
url: "translation/json-request-details"
title: "JSON Request Details"
productName: "GroupDocs.Translation Cloud"
weight: 5
description: ""
keywords: ""
---

User should put in the requests body following information to translate a document:

* **format** — format of file for translation (ex: docx)
* **outformat** — format of translated file (ex: pdf)
* **pair** — language translation pair (ex: en-fr)
* **name** — name of file to translate (ex: test.docx)
* **folder** — folder of file to translate (ex: translate) 
* **savepath** — folder for translated file (ex: translated)
* **savefile** — name of translated file (ex: translation.docx)
* **storage** — name of storage
* **masters** — if masters slides should be translated (only for presentations, pass true or false)
* **elements** — slide pages to translate (only for presentations, pass empty list to translate whole presentation)

To translate plain text the following information should be put in the requests body:

* **pair** — language translation pair (ex: en-fr)
* **text** — text to translate (ex: hello world)