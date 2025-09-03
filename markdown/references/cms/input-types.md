# CMS Input Types Documentation

> This document is work in progress and describes a feature that is not released yet.
This document outlines the supported input types in the new CMS system.

---

## Input Types

### text

Single-line plain text input without formatting.

**Settings**:

- `validationMaxLength`: Maximum number of characters allowed (e.g. `50`).
- `validationMinLength`: Minimum number of characters required (e.g. `3`).
- `validationRegex`: Pattern the text must match (e.g. `^[A-Z]+$`).
- `validationIsEmail`: Checks for a valid e-mail address.
- `validationIsHttpsUrl`: Checks for a valid https url. 


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
- `useTypographySelection`: If enabled, instead of font-size the user can select a typography (headline1, headline 2, ...)

---

### richText

Multi-line WYSIWYG editor with rich formatting.

**Settings**:

- _None_

---

### html

HTML editor with syntax highlighting.

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

Shows a group of inputs that allow user to select products in different ways. For example products that fit a specific search term, products of a specific brand/category or specific products via a list of product codes.

**Settings**:

- _None_

### productSelector

Shows a selector where user can easily select one or multiple products, based on setting. If multiple products are selected, the order can also be changed via drag&drop.

**Settings**:

 - `allowMultipleProducts`: If multiple products or only one product can be selected (boolean)

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
