---
stoplight-id: 1s2it6cza4o4v
---

# Search
The Search page contains search results.

## How to customize
### Portals
The Search page offers a similar experience to the Category page. This is why it shares [Product List Item](/references/engage/portals/product-list-item) portals.

## How to link
You can link directly to the search page results.

```jsx
import React from 'react';
import { Link } from '@shopgate/engage/components';
import { SEARCH_PATH } from '@shopgate/engage/search';

/**
 * @param {string} searchPhrase Plain text search phrase
 **/
const Component = ({ searchPhrase }) => (
    <Link href={`${SEARCH_PATH}?s=${encodeURIComponent(searchPhrase)}`}>Open search results for {searchPhrase}</Link>
);

export default Component;
```