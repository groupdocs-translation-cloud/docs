---
id: "supported-document-formats"
weight: 20
date: "2023-10-05"
author: "Vladimir Lapin"
type: docs
url: translation/supported-file-formats
aliases:
- translation/supported-document-formats
productName: "GroupDocs.Translation Cloud"
title: Supported file formats
description: A complete list of file formats that can be translated using GroupDocs.Translation Cloud.
keywords:
- format
- extension
- conversion
- source
- target
---

GroupDocs.Translation Cloud can translate files in all popular formats while accurately preserving layout, structure, and formatting.

Document | Extensions | Description
-------- | ---------- | -----------
Plain text | .TXT | Plain text files or text in the form of lines.
Portable Document Format | .PDF | An open standard cross-platform format for documents that include formatted text, images, multimedia elements, and more.
HTML page | .HTML, .HTM | The standard markup language for Web pages.
Microsoft Word | .DOCX<br />.DOCM<br />.DOC | Microsoft Word 97-2021 and Microsoft 365 documents, including macro-enabled documents.
Rich Text Format | .RTF | Popular rich text format supported by many word processors in different OS'es.
OpenDocument Text | .ODT | Documents created with a number of open source word processing applications, such as _Writer_ from Apache OpenOffice and LibreOffice.
Microsoft Excel | .XLSX<br />.XLSM<br />.XLS | Microsoft Excel and Microsoft 365 workbooks, including macro-enabled workbooks.
OpenDocument Spreadsheet | .ODS | Spreadsheets created with a number of open source applications, such as _Calc_ from Apache OpenOffice and LibreOffice.
Comma-separated values | .CSV | Tabular data in a plain text format that uses commas as a separator between values.
Tab-separated values | .TSV | Tabular data in a plain text format that uses tabs as a delimiter between values.
Microsoft PowerPoint | .PPTX<br />.PPTM<br />.PPT | Microsoft PowerPoint 97-2021 and Microsoft 365 PowerPoint presentations, including macro-enabled presentations.
OpenDocument Presentation | .ODP | Presentations created with a number of open source applications, such as _Impress_ from Apache OpenOffice and LibreOffice.
Images | .JPG, .PNG, .TIFF, .PDF, and more | Scans or photos, including scanned (image-only) PDF.
Markdown | .MD | Plain text files formatted using one of the dialects of the Markdown language (including Markdown with Hugo syntax).
Resource files | .RESX | Microsoft .NET application resources (text only).

**Note:** We cannot guarantee that translated documents will be fully compatible with applications other than those in which the original document was created. For example, if the original document was created in Microsoft Office 2016, we recommend that you open the translated document in the same or newer version of Office applications.

## Conversion

In addition to translation, GroupDocs.Translation Cloud can save the translated document in various file formats other than the original, with formatting preserved (where applicable).

Source file format | Converted file format
------------------ | ---------------------
.PDF               | .DOCX<br />.PPTX<br />.HTML<br />.SVG<br />.XPS
.DOCX              | .RTF<br />.HTML<br />.ODT<br />.TXT<br />.MD<br />.PDF<br />.TIFF<br />.SVG<br />.XPS
.DOC               | .DOCX<br />.RTF<br />.HTML<br />.ODT<br />.TXT<br />.MD<br />.PDF<br />.TIFF<br />.SVG<br />.XPS
.ODT               | .DOCX<br />.RTF<br />.HTML<br />.ODT<br />.TXT<br />.MD<br />.PDF<br />.TIFF<br />.SVG<br />.XPS
.RTF               | .DOCX<br />.RTF<br />.HTML<br />.ODT<br />.TXT<br />.MD<br />.PDF<br />.TIFF<br />.SVG<br />.XPS
.XLSX              | .DOCX<br />.XLSB<br />.PPTX<br />.HTML<br />.MD<br />.PDF<br />.TIFF<br />.XPS<br />.ODS
.XLS               | .XLSX<br />.DOCX<br />.XLSB<br />.PPTX<br />.HTML<br />.MD<br />.PDF<br />.TIFF<br />.XPS<br />.ODS
.ODS               | .XLSX<br />.DOCX<br />.XLSB<br />.PPTX<br />.HTML<br />.MD<br />.PDF<br />.TIFF<br />.XPS
.CSV               | .XLSX<br />.DOCX<br />.XLSB<br />.PPTX<br />.HTML<br />.MD<br />.PDF<br />.TIFF<br />.XPS<br />.ODS
.TSV               | .XLSX<br />.DOCX<br />.XLSB<br />.PPTX<br />.HTML<br />.MD<br />.PDF<br />.TIFF<br />.XPS<br />.ODS
.PPTX              | .PPTX<br />.PDF<br />.TIFF<br />.HTML<br />.XPS<br />.ODP
.PPT               | .PPT<br />.PPTX<br />.PDF<br />.TIFF<br />.HTML<br />.XPS<br />.ODP
.ODP               | .PPTX<br />.PDF<br />.TIFF<br />.HTML<br />.XPS<br />.ODP
.MD                | .HTML<br />.PDF<br />.DOCX<br />.TIFF<br />.XPS
