---
id: "supported-formats"
url: "translation/supported-formats"
title: "Supported Formats"
productName: "GroupDocs.Translation Cloud"
weight: 3
description: ""
keywords: ""
---

GroupDocs.Translation Cloud allows to translate Microsoft Word and Excel documents. User should specify format of document to translate putting in the request’s body:

* **extension of word file (docx / docm / doc / rtf)** — to translate Microsoft Word document
* **extension of excel file (xlsx / xlsm / xls / csv / tsv)** — to translate Microsoft Excel workbook
* **extension of powerpoint file (ppt / pptx / pptm)** — to translate Microsoft PowerPoint presentation
* **extension of PDF file (pdf)** — to translate Adobe PDF document
* **extensiion of Markdown file (md)** - to translate Markdown file
* **extension of OpenDocument files (odt / ods / odp)** — to translate files of OpenDocument format
* **hugo** — to translate Markdown file with Hugo syntax

Additionally, user could obtain translated file in any other format available for conversion. Just specify output format of translated document putting file extension in the request's body:

* **doc, docx, odt, rtf** — docx, rtf, html, odt, txt, md, pdf, tiff, svg, xps
* **xls, xlsx, ods, csv, tsv** — xlsx, xlsb, html, pdf, xps, ods, md, docx, pptx, tiff
* **ppt, pptx, odp** — pptx, pdf, tiff, html, xps, odp
* **pdf** — docx, pptx, html, xps, svg
* **md** - html, pdf, docx, tiff, xps

Remarks:

1. Conversion from doc / xls / ppt to docx / xlsx / pptx is supported but not vice versa
2. Document with macros could be saved only using the same format, i.e. docm / xlsm / pptm
3. If format is not supported or there is a mistake, translated file would be saved using the same format under specified name in request, i.e. translated.png.docx
4. Default options are used for file conversion, if result is unsatisfactory, convert it with custom options using corresponding Aspose product 
5. CSV and TSV files are treated as Excel workbook, so the result of conversion will be exactly the same as for xls(x) file
6. Conversion of files with Hugo syntax is not supported, as conversion won't render desirable output.