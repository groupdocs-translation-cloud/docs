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
* **separator** - delimiter if you translate CSV file, "," by default
* **shortcodedict** - dictionary for Hugo short code syntax translation, where **key** is zero based index of short code and **value** is list of short code parameters names, which values should be translated, or zero based parameters indexes, converted to strings, if you use positional short codes.
* **frontmatterdict** - dictionary for Hugo front matter syntax, where **key** is zero based index of front matter and **value** is list of list of strings, where list of strings is a path to the value, that requires translation. 
* **optimizepdffontsize** - if set to `true`, font size of every paragraph will be selected to fit paragraph's rectangle, in other case font size of every paragraph will be slightly decreased by the same multiplier. 

To translate plain text the following information should be put in the requests body:

* **pair** — language translation pair (ex: en-fr)
* **text** — text to translate (ex: hello world)
* **type** - by deafult is equal to "text" and corresponds to plain text, if text contains Markdown syntax, should be equal to "md".