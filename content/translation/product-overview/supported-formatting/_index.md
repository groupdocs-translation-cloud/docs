---
id: "supported-formatting"
weight: 30
date: "2023-10-05"
author: "Vladimir Lapin"
type: docs
url: translation/supported-formatting
aliases:
- translation/supported-formatting
productName: "GroupDocs.Translation Cloud"
title: Supported content formatting
description: A list of layout and structural elements of the source document that are guaranteed to be translated by GroupDocs.Translation Cloud.
keywords:
- format
- layout
- structure
- element
- source
- target
---

GroupDocs.Translation Cloud preserves layout, structure, and formatting when translating even the most complex documents. Below is the list of layout and structural elements of the source document that are guaranteed to be processed:

## Microsoft Word / ODT documents

Most paragraph styles are retained. Inline styles may be lost depending on the grammar and structure of the target language.

- Headings;
- Paragraphs;
- Lists;
- Tables;
- Headers and footers;
- Footnotes and end-notes;
- Image captions.

## Microsoft Excel / ODS spreadsheets

- Cells;
- Charts;
- Pivot tables.

Inline text styles in cells will be lost.

## Microsoft PowerPoint / ODP presentations

- Text frames;
- Charts;
- Tables;
- Headers and footers;
- Notes and comments;
- Slides;
- Master slides.

## Markdown

- Basic GitHub formatting syntax;
- Hugo syntax structures.

## PDF

- Text blocks (paragraphs);
- Tables.

Inline text styles will be lost.
