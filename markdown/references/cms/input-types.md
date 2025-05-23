---
internal: true
---

# CMS Input Types Documentation

This document outlines the supported input types in the CMS system.

---

## List of input types

- [Text](#text)
- [TextArea](#textarea)
- [TextWithFormatting](#textwithformatting)
- [RichText](#richtext)
- [RichTextArea](#richtextarea)
- [URL](#url)
- [Number](#number)
- [Boolean](#boolean)
- [Select](#select)
- [MultiSelect](#multiselect)
- [DateTime](#datetime)
- [Date](#date)
- [Link](#link)
- [ProductList](#productlist)
- [Image](#image)
- [TextWithFormatting Block](#textwithformatting-block)
- [Category](#category)
- [DateFromTo](#datefromto)

---

## Input Types

### text

Single-line plain text input without formatting.

**Settings**:

- `validationMaxLength`: Maximum number of characters allowed (e.g. `50`).
- `validationMinLength`: Minimum number of characters required (e.g. `3`).
- `validationRegex`: Pattern the text must match (e.g. `^[A-Z]+$`).

---

### textArea

Multi-line plain text input without formatting.

**Settings**:

- `validationMaxLength`: Maximum number of characters allowed (e.g. `50`).
- `validationMinLength`: Minimum number of characters required (e.g. `3`).
- `validationRegex`: Pattern the text must match (e.g. `^[A-Z]+$`).

---

### textWithFormatting

Formatted text input like headlines. Allows bold, size, etc.

**Settings**:

- `validationMaxLength`: Maximum number of characters allowed (e.g. `50`).
- `validationMinLength`: Minimum number of characters required (e.g. `3`).
- `validationRegex`: Pattern the text must match (e.g. `^[A-Z]+$`).

---

### richText

Multi-line WYSIWYG editor with rich formatting.

**Settings**:

- _None_

---

### number

Numeric input field accepting integers and decimals.

- **Settings**:

  - `validationMinValue`: Minimum numeric value allowed (e.g. `0`).
  - `validationMaxValue`: Maximum value allowed (e.g. `1000`).
  - `validationRegex`: Format for numbers if specific patterns are required.
  - `numberOfDecimals`: Number of decimal places allowed (e.g. `2`).

---

### boolean

Checkbox input (true/false).

**Settings**:

- _None_

---

### select

Dropdown for single selection.

- **Settings**:

  - `options`: Array of `{ value, label }` pairs (e.g. `{ value: 'sort_desc', label: 'Descending' }`).

---

### category

Shows a selector where user can choose a category.

**Settings**:

- _None_

### products

Shows a selector where user can define a list of products, e.g. all products that fit a specific search term, all products of a specific brand/category or specific products via a list of product codes.

**Settings**:

- _None_

### dateTime

Selector for both date and time.

**Settings**:

- _None_

---

### link

User can generate a link in different ways, e.g. by selecting a specific page, product, category, providing a full URL for external link, or an internal app-path.

**Settings**:

- _None_

---

### image

Image including alt text.

**Settings**:

- _None_
