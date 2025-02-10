---
stoplight-id: z7p362xrv7lq6
---

# NavMenu

Contains all portals for the navigation menu in the GMD theme and the "More" page of the iOS theme.

## Default Portal Props

The following React components are passed to all of the NavMenu Portals as Props.

- `Section`: Creates a section with potentially multiple entries and a dedicated section title. The `Logout` and `My Account` portals do not get this Prop.
- `Item`: Inserts an entry into an already existing section or creates the entries within a custom section.

## Content

| Name | Description | Props |
| - | - | - |
| `nav-menu.content.before` | Components are rendered **before** the NavMenu contents. | Default Portal Props|
| `nav-menu.content.after` | Components are rendered **after** the NavMenu contents. | Default Portal Props|

## Entries

### Home (only GMD)

| Name | Description | Props |
| - | - | - |
| `nav-menu.home.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.home` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.home.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Categories (only GMD)

| Name | Description | Props |
| - | - | - |
| `nav-menu.categories.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.categories` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.categories.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Favorites (only GMD)

| Name | Description | Props |
| - | - | - |
| `nav-menu.favorites.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.favorites` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.favorites.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Cart (only GMD)

| Name | Description | Props |
| - | - | - |
| `nav-menu.cart.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.cart` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.cart.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Scanner (only GMD)

| Name | Description | Props |
| - | - | - |
| `nav-menu.scanner.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.scanner` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.scanner.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Shipping

| Name | Description | Props |
| - | - | - |
| `nav-menu.shipping.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.shipping` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.shipping.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Payment

| Name | Description | Props |
| - | - | - |
| `nav-menu.payment.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.payment` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.payment.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Terms

| Name | Description | Props |
| - | - | - |
| `nav-menu.terms.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.terms` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.terms.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Privacy Policy

| Name | Description | Props |
| - | - | - |
| `nav-menu.privacy.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.privacy` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.privacy.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Return Policy

| Name | Description | Props |
| - | - | - |
| `nav-menu.return-policy.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.return-policy` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.return-policy.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Imprint

| Name | Description | Props |
| - | - | - |
| `nav-menu.imprint.before` | Components are rendered **before** the NavMenu entry. | Default Portal Props|
| `nav-menu.imprint` | Components **replace** the NavMenu entry. | Default Portal Props|
| `nav-menu.imprint.after` | Components are rendered **after** the NavMenu entry. | Default Portal Props|

### Logout

| Name | Description | Props |
| - | - | - |
| `nav-menu.logout.before` | Components are rendered **before** the NavMenu entry. | `Item` - A React component which can be used as an entry for a section. |
| `nav-menu.logout` | Components **replace** the NavMenu entry. | `Item` - A React component which can be used as an entry for a section. |
| `nav-menu.logout.after` | Components are rendered **after** the NavMenu entry. | `Item` - A React component which can be used as an entry for a section. |

## Sections

### Store Information

The Store Information Portal wraps multiple store-related entries of the Navigation Menu. Within the the `iOS` theme, the Portal wraps all available entries: `shipping`, `payment`, `terms`, `privacy`, `return-policy` and `imprint`. However, in the GMD theme, the list is split into two sections which are wrapped by the `nav-menu.store-information-about` and the `nav-menu.store-information-more` Portal.

| Name | Description | Props |
| - | - | - |
| `nav-menu.store-information.before` | Components are rendered **before** the section content. | Default Portal Props|
| `nav-menu.store-information` | Components **replace** the section content. | Default Portal Props|
| `nav-menu.store-information.after` | Components are rendered **after** the section content. | Default Portal Props|

#### Store Information More (GMD only)

Wraps the section containing the `shipping` and `payment` menu entries.

| Name | Description | Props |
| - | - | - |
| `nav-menu.store-information-more.before` | Components are rendered **before** the section content. | Default Portal Props|
| `nav-menu.store-information-more` | Components **replace** the section content. | Default Portal Props|
| `nav-menu.store-information-more.after` | Components are rendered **after** the section content. | Default Portal Props|

#### Store Information About (GMD only)

Wraps the whole section containing the `terms`, `privacy`, `return-policy` and `imprint` menu entries.

| Name | Description | Props |
| - | - | - |
| `nav-menu.store-information-about.before` | Components are rendered **before** the section content. | Default Portal Props|
| `nav-menu.store-information-about` | Components **replace** the section content. | Default Portal Props|
| `nav-menu.store-information-about.after` | Components are rendered **after** the section content. | Default Portal Props|

### Content (iOS only)

Wraps the `quicklinks`, `store-info` and `my-account` section.

| Name | Description | Props |
| - | - | - |
| `nav-menu.content.before` | Components are rendered **before** the section content. | Default Portal Props|
| `nav-menu.content.after` | Components are rendered **after** the section content. | Default Portal Props|

### User Menu (iOS only)

Wraps the NavMenu login and logout entries.

| Name | Description | Props |
| - | - | - |
| `user-menu.container.before` | Components are rendered **before** the section content. | Default Portal Props|
| `user-menu.container` | Components **replace** the section content. | Default Portal Props|
| `user-menu.container.after` | Components are rendered **after** the section content. | Default Portal Props|

#### My Account (iOS only)

Wraps the `logout` entry on iOS.

| Name | Description | Props |
| - | - | - |
| `nav-menu.my-account.before` | Components are rendered **before** the section content. | `Item` - A React component which can be used as an entry for a section. |
| `nav-menu.my-account` | Components **replace** the section content. | `Item` - A React component which can be used as an entry for a section. |
| `nav-menu.my-account.after` | Components are rendered **after** the section content. | `Item` - A React component which can be used as an entry for a section. |