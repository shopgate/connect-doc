---
stoplight-id: xpobbokd5aqxp
---

# Search

## Search Suggestions

### Suggestion Props

- `onClick` (Function) - The original click handler applied to the onClick attribute on the item.
- `suggestion` (Object) - The single suggestion, rendered by the item.

| Name                        | Description                                                | Props            |
| --------------------------- | ---------------------------------------------------------- | ---------------- |
| `search.suggestions.before` | Components are rendered **before** the search suggestions. | Suggestion Props |
| `search.suggestions`        | Components **replace** the search suggestions.             | Suggestion Props |
| `search.suggestions.after`  | Components are rendered **after** the search suggestions.  | Suggestion Props |

## Search Suggestions Item

### Item Props

- `className` (string) - The original CSS class applied to the item.
- `onClick` (Function) - The original click handler applied to the onClick attribute on the item.
- `suggestion` (Object) - The single suggestion, rendered by the item.

| Name                            | Description                                                          | Props      |
| ------------------------------- | -------------------------------------------------------------------- | ---------- |
| `search.suggestion-item.before` | Components are rendered **before** a single search suggestion item.  | Item Props |
| `search.suggestion-item`        | Components **replace** a single search suggestion item.              | Item Props |
| `search.suggestion-item.after`  | Components are rendered **after** a single search suggestion item.   | Item Props |

## Search Suggestions Item Content

| Name                                    | Description                                                               | Props                                                                |
| --------------------------------------- | ------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `search.suggestion-item-content.before` | Components are rendered **before** the search suggestion item's content.  | `suggestion` (Object) - The single suggestion, rendered by the item. |
| `search.suggestion-item-content`        | Components **replace** the search suggestion item's content.              | `suggestion` (Object) - The single suggestion, rendered by the item. |
| `search.suggestion-item-content.after`  | Components are rendered **after** the search suggestion item's content.   | `suggestion` (Object) - The single suggestion, rendered by the item. |