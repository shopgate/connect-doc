# Tutorial: How to integrate a search provider

This tutorial shows you how to integrate a new product search provider into your Shopgate Connect application. This example uses the search provider `Amazon Cloudsearch.`

## Prerequisites
Before beginning this tutorial, complete the following tasks:

- Create a [Shopgate Developer Account](https://developer.shopgate.com/admin/login).
- Complete the Shopgate [Getting Started](markdown/introduction/index.md) instructions.
- Create a new backend extension with the Shopgate Connect SDK.
- Optional: Complete Hello World Tutorial [markdown/tutorials/starter/hello-world/overview.md]

## Pipelines
To integrate a new search provider, you must have the following pipelines in your applications:

### Filter
- **shopgate.catalog.getFilters.v1**: provides a list of available filters for a set of products
- **shopgate.catalog.getProductsByFilter.v1**: provides a filtered list of products in a category

### Search
- **shopgate.catalog.getProductsBySearchPhrase.v1**: provides a list of products that match the search phrase
- **shopgate.catalog.getProductsBySearchPhraseAndFilter.v1**: provides a list of products that match the search phrase and the filter

### Suggestions
- **shopgate.catalog.getSearchSuggestions.v1**: provides a list of suggestions based on the user's search input (minimum two characters)


## Integration
> **Note:** The following steps use the example extension name `@awesomeAgency/cloudsearch`. In your application, use your own extension name.

The search integration contains the following search options:
- Search by filters
- Search by a phrase
- Search by a phrase and filter the result
- Show search suggestions

### Integrate Pipeline for Available Filters

#### Provide the Pipeline to Fetch Filters

The first step to integrate filters is to provide the following pipeline: [`shopgate.catalog.getFilters.v1`](https://developer.shopgate.com/references/connect/shopgate-pipelines/search/shopgate.catalog.getfilters.v1) . This pipeline returns available filters for a subset of products (such as products in a category, the result of a product search, or all products).

To begin, create the file `shopgate.catalog.getFilters.v1.json` in the `pipelines` directory of the extension. Copy the following content into the `shopgate.catalog.getFilters.v1.json` file:
```json
// pipelines/shopgate.catalog.getFilters.v1.json
{
  "version": "1",
  "pipeline": {
    "id": "shopgate.catalog.getFilters.v1",
    "public": true,
    "input": [
      {
        "id": "1",
        "key": "categoryId",
        "optional": true
      },
      {
        "id": "2",
        "key": "searchPhrase",
        "optional": true
      },
      {
        "id": "3",
        "key": "filters",
        "optional": true
      }
    ],
    "steps": [
    ],
    "output": [
      {
        "id": "1000",
        "key": "filters"
      }
    ]
  }
}
```
These pipeline parameters follow the default Shopgate pipeline specification. The inputs are `categoryId` or `searchPhrase`. The app calls the pipeline with either both inputs or only one input set. The output is an object containing available filters. For the structure of the object, refer to ["getFilter" reference](/references/connect/shopgate-pipelines/search/shopgate.catalog.getfilters.v1).


Next, add a step to the pipeline to perform the request to the search provider. Copy the following step definition to the `steps` array:

```json
{
  "type": "extension",
  "id": "@awesomeAgency/cloudsearch",
  "path": "@awesomeAgency/cloudsearch/getFilters.js",
  "input": [
    {
      "id": "1",
      "key": "categoryId",
      "optional": true
    },
    {
      "id": "2",
      "key": "searchPhrase",
      "optional": true
    },
    {
      "id": "3",
      "key": "filters",
      "optional": true
    }
  ],
  "output": [
    {
      "id": "1000",
      "key": "filters"
    }
  ]
}
```

The pipeline should look as follows:
```json
// pipelines/shopgate.catalog.getFilters.v1.json
{
  "version": "1",
  "pipeline": {
    "id": "shopgate.catalog.getFilters.v1",
    "public": true,
    "input": [
      {
        "id": "1",
        "key": "categoryId",
        "optional": true
      },
      {
        "id": "2",
        "key": "searchPhrase",
        "optional": true
      },
      {
        "id": "3",
        "key": "filters",
        "optional": true
      }
    ],
    "steps": [
      {
        "type": "extension",
        "id": "@awesomeAgency/cloudsearch",
        "path": "@awesomeAgency/cloudsearch/getFilters.js",
        "input": [
          {
            "id": "1",
            "key": "categoryId",
            "optional": true
          },
          {
            "id": "2",
            "key": "searchPhrase",
            "optional": true
          },
          {
            "id": "3",
            "key": "filters",
            "optional": true
          }
        ],
        "output": [
          {
            "id": "1000",
            "key": "filters"
          }
        ]
      }
    ],
    "output": [
      {
        "id": "1000",
        "key": "filters"
      }
    ]
  }
}
```

#### Develop the Step Logic

To search for products with your search engine provider, you need to implement the step logic.

This implementation depends on how your search engine functions. The following code uses Amazon CloudSearch as an example. Adapt your integration to your specific search engine.

##### Integrate Request

After adding the step into the pipeline, you must write the step code. The step code must provide all available filters as an output. The inputs are the same as from the pipeline: `categoryId` or `searchTerm`.

Create an empty step with the name `getFilters.js` in the `extension` directory:
```javascript=
// extension/getFilters.js
modules.exports = (context, input) => {
    // Add your code here
}
```

Next, you need to implement the request to the search engine. This tutorial uses the fake URL `https://some-search-tdzf81pfwhdi543mdpc3vrbqwd.eu-west-1.cloudsearch.amazonaws.com/2013-01-01/search`.

Open a new terminal, navigate to the extension directory (`<workspace folder>/extensions/@myAwesomeAgency-cloudsearch/extensions`) and run `npm install request request-promise-native`.

Then, integrate the request logic. The following example shows an integration of the default Shopgate search:
```javascript
// extension/getFilters.js
const request = require('request-promise-native')
module.exports = async (context, input) => {

  let fq = `shop_number:${context.config.shopNumber}`
  if (input.categoryId) {
    fq = `(and shop_number:${context.config.shopNumber} (prefix field=categoryId \'${input.categoryId}\'))`
  }

  let q = 'matchall'
  if (input.searchPhrase) {
    q = `(or (term boost=2 '${input.searchPhrase}') (prefix '${input.searchPhrase}') item_numbers:'${input.searchPhrase}')`
  }

  const query = {
    return: 'uid',
    'q.options': { fields: [ 'name^2',
        'child_names',
        'item_numbers',
        'tags',
        'categories_searchable',
        'attributes_searchable',
        'options_searchable',
        'properties_searchable',
        'manufacturer_searchable',
      'name_normalized^0.5' ] },
    fq,
    'q.parser': 'structured',
    q,
    size: 0, // get no results just the filter
    'facet.attributes': { sort: 'bucket', size: 5000 },
    'facet.options': { sort: 'bucket', size: 5000 },
    'facet.properties': { sort: 'bucket', size: 5000 },
    'facet.categories': { sort: 'count', size: 20 },
    'facet.manufacturer': { sort: 'bucket', size: 5000 },
    'facet.display_amount': { sort: 'bucket', size: 5000 },
  sort: '_score desc' }

  const result = await request({
    url: 'https://some-search-tdzf81pfwhdi543mdpc3vrbqwd.eu-west-1.cloudsearch.amazonaws.com/2013-01-01/search',
    qs: query
  })
  // TODO: Add logic to extract filter
}
```

##### Extract the Filter Logic
After the step requests the filter from CloudSearch, map the result to the predefined structure. For more information, see the [`getFilters` Pipeline reference](https://developer.shopgate.com/references/connect/shopgate-pipelines/search/shopgate.catalog.getfilters.v1).

> **Note:** The logic to extract the filter strongly depends on the real data in the search engine. This tutorial does not show how the mapping is done.

### Integrate Product Filtering
After you integrate the `getFilters` pipeline, the theme automatically fetches all filters ofon a category and search view. When the user applies one of these filters, the pipeline `shopgate.catalog.getProductsByFilter.v1`[Add reference] is called.

The input parameters include the selected filter and optionally the category ID, if the filter is applied on a category. The output must include the product collection matching the selected filter and the total count of products.

The next step describes the steps to provide the pipeline.

#### Provide the Pipeline to Get Products Based on a Filter

The pipeline `shopgate.catalog.getProductsByFilter.v1` consists of two parts. The first part delivers all product IDs, and the second part uses these IDs to fetch all product data.

The functionality of the first part needs to be provided by your extension. For more detailed information, see [Add link for products pipeline guide]. The platform provides the functionality of the second part by default, in the form of the pipeline `shopgate.catalog.getProductsByIds`.

To start with the pipeline, create a json file with the name `shopgate.catalog.getProductsByFilter.v1.json` in the `pipeline` directory of your extension. Copy the following content into the file:
```json
// pipelines/shopgate.catalog.getProductsByFilter.v1.json
{
  "version": "1",
  "pipeline": {
    "id": "shopgate.catalog.getProductsByFilter.v1",
    "public": true,
    "input": [
      {
        "id": "1",
        "key": "offset",
        "optional": true
      },
      {
        "id": "2",
        "key": "limit",
        "optional": true
      },
      {
        "id": "3",
        "key": "sort",
        "optional": true
      },
      {
        "id": "4",
        "key": "filters"
      },
      {
        "id": "5",
        "key": "categoryId",
        "optional": true
      },
      {
        "id": "8",
        "key": "skipHighlightLoading",
        "optional": true
      },
      {
        "id": "9",
        "key": "skipLiveshoppingLoading",
        "optional": true
      },
      {
        "id": "15",
        "key": "showInactive",
        "optional": true
      },
      {
        "id": "750",
        "key": "sgxsMeta"
      }
    ],
    "output": [
      {
        "id": "1000",
        "key": "totalProductCount"
      },
      {
        "id": "100",
        "key": "products"
      }
    ],
    "steps": [
      {
        "id": "@awesomeAgency/cloudsearch",
        "path": "@awesomeAgency/cloudsearch/getProductsByFilter.js",
        "type": "extension",
        "input": [
          {
            "id": "1",
            "key": "offset",
            "optional": true
          },
          {
            "id": "2",
            "key": "limit",
            "optional": true
          },
          {
            "id": "3",
            "key": "sort",
            "optional": true
          },
          {
            "id": "4",
            "key": "filters"
          },
          {
            "id": "5",
            "key": "categoryId",
            "optional": true
          }
        ],
        "output": [
          {
            "id": "20",
            "key": "productIds",
            "optional": true
          },
          {
            "id": "1000",
            "key": "totalProductCount"
          }
        ]
      },
      {
        "type": "pipeline",
        "id": "shopgate.catalog.getProductsByIds.v1",
        "input": [
          {
            "id": "20",
            "key": "productIds",
            "optional": true
          },
          {
            "id": "8",
            "key": "skipHighlightLoading",
            "optional": true
          },
          {
            "id": "9",
            "key": "skipLiveshoppingLoading",
            "optional": true
          },
          {
            "id": "15",
            "key": "showInactive",
            "optional": true
          },
          {
            "id": "750",
            "key": "sgxsMeta"
          }
        ],
        "output": [
          {
            "id": "100",
            "key": "products"
          }
        ]
      }
    ]
  }
}
```
The pipeline file calls the step `extension/getProductsByFilter.js` to fetch the product IDs and the total count first. Then, the pipeline forwards these parameters to `shopgate.catalog.getProductsById.v1`.

#### Develop the Step Logic
To complete this section, you must implement the step referenced above. This step has the following input parameters:
- filters
- categoryId (optional)
- offset (optional)
- limit (optional)
- sort (optional)

This step also includes the following output parameters:
- productIds
- totalProductCount

Create a step with the file name `getProductsByFilter.js` in the `extension` directory of your extension. Then, integrate the request logic. The following example is an integration of the default Shopgate search:
```javascript
// extension/getProductsByFilter.js
const request = require('request-promise-native')
module.exports = async (context, input) => {

  const filterString = mapFilter(input.filters)

  let fq = `(and shop_number:${context.config.shopNumber} ${filterString})`
  if (input.categoryId) {
    fq = `(and shop_number:${context.config.shopNumber} (prefix field=categoryId \'${input.categoryId}\') ${filterString})`
  }

  const sort = mapSort(input.sort)

  const query = {
    return: 'uid',
    'q.options': { fields: [ 'name^2',
        'child_names',
        'item_numbers',
        'tags',
        'categories_searchable',
        'attributes_searchable',
        'options_searchable',
        'properties_searchable',
        'manufacturer_searchable',
      'name_normalized^0.5' ] },
    fq,
    'q.parser': 'structured',
    q: 'matchall',
    size: input.limit || 20, // get no results just the filter
    start: input.offset || 0,
    'facet.attributes': { sort: 'bucket', size: 5000 },
    'facet.options': { sort: 'bucket', size: 5000 },
    'facet.properties': { sort: 'bucket', size: 5000 },
    'facet.categories': { sort: 'count', size: 20 },
    'facet.manufacturer': { sort: 'bucket', size: 5000 },
    'facet.display_amount': { sort: 'bucket', size: 5000 },
    sort
  }

  const result = await request({
    url: 'https://some-search-tdzf81pfwhdi543mdpc3vrbqwd.eu-west-1.cloudsearch.amazonaws.com/2013-01-01/search',
    qs: query
  })
  return {
    productIds: result.hits.hit.map((hit) => {
      return hit.fields.uid
    }),
    totalProductCount: result.hits.found
  }
}
```

> **Note:** The reference implementation above is an example for the Shopgate default search. Adapt it for other search engines, search providers, and use cases.

### Integrate Search
In this step, implement the search. When a user enters a search term into the search box and clicks the search button, the pipeline `shopgate.catalog.getProductsBySearchPhrase.v1` is called.

It receives the search term as an input parameter. The output must include the product collection that matches the selected filter and the total count of products.

#### Provide the Pipeline to Fetch Products Based on a Search Term
This pipeline is split into two parts like the other `shopgate.catalog.getProducts*` pipelines. You only need to implement fetching of the product IDs.

Create a new pipeline with the filename `shopgate.catalog.getProductsBySearchPhrase.v1.json` in the `pipelines` directory of the extension. Copy the following content into the file:
```json
// pipelines/shopgate.catalog.getProductsBySearchPhrase.v1.json
{
  "version": "1",
  "pipeline": {
    "id": "shopgate.catalog.getProductsBySearchPhrase.v1",
    "public": true,
    "input": [
      {
        "id": "1",
        "key": "offset",
        "optional": true
      },
      {
        "id": "2",
        "key": "limit",
        "optional": true
      },
      {
        "id": "3",
        "key": "sort",
        "optional": true
      },
      {
        "id": "4",
        "key": "searchPhrase"
      },
      {
        "id": "8",
        "key": "skipHighlightLoading",
        "optional": true
      },
      {
        "id": "9",
        "key": "skipLiveshoppingLoading",
        "optional": true
      },
      {
        "id": "15",
        "key": "showInactive",
        "optional": true
      },
      {
        "id": "750",
        "key": "sgxsMeta"
      }
    ],
    "output": [
      {
        "id": "1000",
        "key": "totalProductCount"
      },
      {
        "id": "100",
        "key": "products"
      }
    ],
    "steps": [
      {
        "type": "extension",
        "id": "@awesomeAgency/cloudsearch",
        "path": "@awesomeAgency/cloudsearch/getProductsBySearchPhrase.js",
        "input": [
          {
            "id": "1",
            "key": "offset",
            "optional": true
          },
          {
            "id": "2",
            "key": "limit",
            "optional": true
          },
          {
            "id": "3",
            "key": "sort",
            "optional": true
          },
          {
            "id": "4",
            "key": "searchPhrase"
          }
        ],
        "output": [
          {
            "id": "10",
            "key": "productIds"
          },
          {
            "id": "1000",
            "key": "totalProductCount"
          }
        ]
      },
      {
        "type": "pipeline",
        "id": "shopgate.catalog.getProductsByIds.v1",
        "input": [
          {
            "id": "10",
            "key": "productIds",
            "optional": true
          },
          {
            "id": "8",
            "key": "skipHighlightLoading",
            "optional": true
          },
          {
            "id": "9",
            "key": "skipLiveshoppingLoading",
            "optional": true
          },
          {
            "id": "15",
            "key": "showInactive",
            "optional": true
          },
          {
            "id": "750",
            "key": "sgxsMeta"
          }
        ],
        "output": [
          {
            "id": "100",
            "key": "products"
          }
        ]
      }
    ]
  }
}
```

#### Develop the Step Logic
This pipeline starts with the first step `getProductsBySearchPhrase.js` and includes the following parameters:
- searchPhrase
- offset (optional)
- limit (optional)
- sort (optional)

This pipeline also has the following output parameters:
- productIds
- totalProductCount

Create the file `getProductsByFilter.js` in the `extension` directory of your extension.

Then, integrate the request logic to retrieve all product IDs of products matching the search phrase. The following example shows an integration of the default Shopgate search:

```javascript
const request = require('request-promise-native')
module.exports = async (context, input) => {
  const sort = mapSort(input.sort)

  const query = {
    return: 'uid',
    'q.options': { fields: [ 'name^2',
        'child_names',
        'item_numbers',
        'tags',
        'categories_searchable',
        'attributes_searchable',
        'options_searchable',
        'properties_searchable',
        'manufacturer_searchable',
      'name_normalized^0.5' ] },
    fq: `shop_number:${context.config.shopNumber}`,
    'q.parser': 'structured',
    q: `(or (term boost=2 '${input.searchPhrase}') (prefix '${input.searchPhrase}') item_numbers:'${input.searchPhrase}')`,
    size: input.limit || 20, // get no results just the filter
    start: input.offset || 0,
    'facet.attributes': { sort: 'bucket', size: 5000 },
    'facet.options': { sort: 'bucket', size: 5000 },
    'facet.properties': { sort: 'bucket', size: 5000 },
    'facet.categories': { sort: 'count', size: 20 },
    'facet.manufacturer': { sort: 'bucket', size: 5000 },
    'facet.display_amount': { sort: 'bucket', size: 5000 },
    sort
  }

  const result = await request({
    url: 'https://some-search-tdzf81pfwhdi543mdpc3vrbqwd.eu-west-1.cloudsearch.amazonaws.com/2013-01-01/search',
    qs: query
  })
  return {
    productIds: result.hits.hit.map((hit) => {
      return hit.fields.uid
    }),
    totalProductCount: result.hits.found
  }
}
```

> **Note:** The reference implementation above is an example for the Shopgate default search. Adapt your integration to your specific search engine, search providers, and use cases.


### Integrate Filtering of Search Results

By default, Shopgate's solution allows the end customer to filter search results. It combines searching with filtering. If a user applies a filter on a search result, the pipeline `shopgate.catalog.getProductsBySearchPhraseAndFilter.v1` is called.

#### Provide the Pipeline to Fetch Products Based on a Search Term and a Filter
Because this pipeline is similar to the previous pipelines, the structure is the same.

Create the file `shopgate.catalog.getProductsBySearchPhraseAndFilter.v1.json` in the `pipeline` directory of your extension.
Copy the following content into the file:
```json
// pipelines/shopgate.catalog.getProductsBySearchPhraseAndFilter.v1.json
{
  "version": "1",
  "pipeline": {
    "id": "shopgate.catalog.getProductsBySearchPhraseAndFilter.v1",
    "public": true,
    "input": [
      {
        "id": "1",
        "key": "offset",
        "optional": true
      },
      {
        "id": "2",
        "key": "limit",
        "optional": true
      },
      {
        "id": "3",
        "key": "sort",
        "optional": true
      },
      {
        "id": "4",
        "key": "filters"
      },
      {
        "id": "5",
        "key": "searchPhrase"
      },
      {
        "id": "8",
        "key": "skipHighlightLoading",
        "optional": true
      },
      {
        "id": "9",
        "key": "skipLiveshoppingLoading",
        "optional": true
      },
      {
        "id": "15",
        "key": "showInactive",
        "optional": true
      },
      {
        "id": "750",
        "key": "sgxsMeta"
      }
    ],
    "output": [
      {
        "id": "1000",
        "key": "totalProductCount"
      },
      {
        "id": "100",
        "key": "products"
      }
    ],
    "steps": [
      {
        "type": "extension",
        "id": "@shopgate/search-cloudsearch",
        "path": "@shopgate/search-cloudsearch/steps/getProductBySearchPhraseAndFilter.js",
        "input": [
          {
            "id": "1",
            "key": "offset",
            "optional": true
          },
          {
            "id": "2",
            "key": "limit",
            "optional": true
          },
          {
            "id": "3",
            "key": "sort",
            "optional": true
          },
          {
            "id": "4",
            "key": "filters"
          },
          {
            "id": "6",
            "key": "searchPhrase"
          }
        ],
        "output": [
          {
            "id": "20",
            "key": "productIds"
          },
          {
            "id": "1000",
            "key": "totalProductCount"
          }
        ]
      },
      {
        "type": "pipeline",
        "id": "shopgate.catalog.getProductsByIds.v1",
        "input": [
          {
            "id": "20",
            "key": "productIds",
            "optional": true
          },
          {
            "id": "8",
            "key": "skipHighlightLoading",
            "optional": true
          },
          {
            "id": "9",
            "key": "skipLiveshoppingLoading",
            "optional": true
          },
          {
            "id": "15",
            "key": "showInactive",
            "optional": true
          },
          {
            "id": "750",
            "key": "sgxsMeta"
          }
        ],
        "output": [
          {
            "id": "100",
            "key": "products"
          }
        ]
      }
    ]
  }
}
```
#### Develop the Step Logic
In the next step, create the file `getProductsBySearchPhraseAndFilter.js` in the `extension` directory.

This file has the following input parameters:
- searchPhrase
- filters
- offset (optional)
- limit (optional)
- sort (optional)

This file also has the following output parameters:
- productIds
- totalProductCount

This step needs to fetch all product IDs that match the given searchPhrase and filters. Create the file `getProductsBySearchPhraseAndFilter.js` in the `extension` directory and copy the following content into the file:
```javascript
const request = require('request-promise-native')
module.exports = async (context, input) => {

  const filterString = mapFilter(input.filters)

  let fq = `(and shop_number:${context.config.shopNumber} ${filterString})`
  if (input.categoryId) {
    fq = `(and shop_number:${context.config.shopNumber} (prefix field=categoryId \'${input.categoryId}\') ${filterString})`
  }

  const sort = mapSort(input.sort)

  const query = {
    return: 'uid',
    'q.options': { fields: [ 'name^2',
        'child_names',
        'item_numbers',
        'tags',
        'categories_searchable',
        'attributes_searchable',
        'options_searchable',
        'properties_searchable',
        'manufacturer_searchable',
      'name_normalized^0.5' ] },
    fq: `shop_number:${context.config.shopNumber}`,
    'q.parser': 'structured',
    q: `(or (term boost=2 '${input.searchPhrase}') (prefix '${input.searchPhrase}') item_numbers:'${input.searchPhrase}')`,
    size: input.limit || 20, // get no results just the filter
    start: input.offset || 0,
    'facet.attributes': { sort: 'bucket', size: 5000 },
    'facet.options': { sort: 'bucket', size: 5000 },
    'facet.properties': { sort: 'bucket', size: 5000 },
    'facet.categories': { sort: 'count', size: 20 },
    'facet.manufacturer': { sort: 'bucket', size: 5000 },
    'facet.display_amount': { sort: 'bucket', size: 5000 },
    sort
  }

  const result = await request({
    url: 'https://some-search-tdzf81pfwhdi543mdpc3vrbqwd.eu-west-1.cloudsearch.amazonaws.com/2013-01-01/search',
    qs: query,
    json: true
  })
  return {
    productIds: result.hits.hit.map((hit) => {
      return hit.fields.uid
    }),
    totalProductCount: result.hits.found
  }
}
```
> **Note:** The reference implementation above is an example for the Shopgate default search. Adapt your integration to your specific search engine, search providers, and use cases.

### Integrate Search Suggestions

Another default feature of the Shopgate search is the search suggestion feature. When the user starts to type, the app sends the characters to the backend to retrieve a suggestion of search phrases. The pipeline `shopgate.catalog.getSearchSuggestions.v1` handles these types of requests.

#### Implementing the Pipeline
To integrate this feature, you need to create the pipeline file `shopgate.catalog.getSearchSuggestions.v1.json` in the `pipeline` directory of your extension.

Copy the following content into the file:
```json
{
  "version": "1",
  "pipeline": {
    "id": "shopgate.catalog.getSearchSuggestions.v1",
    "public": true,
    "input": [{"key": "searchPhrase", "id": "1"}],
    "output": [{"key": "suggestions", "id": "1000"}],
    "steps": [
      {
        "type": "extension",
        "id": "@awesomeAgency/cloudsearch",
        "path": "@awesomeAgency/cloudsearch/getSearchSuggestions.js",
        "input": [{"key": "searchPhrase", "id": "1"}],
        "output": [{"key": "suggestions", "id": "1000"}]
      }
    ]
  }
}
```

#### Develop the Step Logic
In this step, implement the step that fetches the search suggestions. The input of this step is the `searchPhrase`. Based on this value, it needs to return an array of suggestions. For more information, review the [`getFilters` Pipeline reference](https://developer.shopgate.com/references/connect/shopgate-pipelines/search/shopgate.catalog.getsearchsuggestions.v1).

Create the step file in the `extension` directory with the name `getSearchSuggestions.js`.
Copy the following content into the file:
```javascript
const request = require('request-promise-native')
module.exports = async (context, input) => {
  const query = {
    'q.parser': 'structured',
    'q.options': '{"fields":["name","child_names"]}',
    size: 100,
    'highlight.name': '{"format":"text","pre_tag":"$start$","post_tag":"$end$"}',
    'highlight.child_names': '{"format":"text","pre_tag":"$start$","post_tag":"$end$"}',
    return: 'name,child_names',
    q: `(or '${input.searchPhrase}' (prefix '${input.searchPhrase}'))`,
    fq: `shop_number:${context.config.shopNumber}`,
  }

  const result = await request({
    uri: 'https://search-shopgate-items-de-hdxp45pgwwdvd4umvpq36rejwe.eu-west-1.cloudsearch.amazonaws.com/2013-01-01/search',
    qs: query,
    qsStringifyOptions: { format: 'RFC1738' },
    timeout: 700,
    json: true })
  return {
    suggestions: result.hits.hit.map((hit) => {
      return hit.fields.name
    }),
  }
}
```

> **Note:** The reference implementation above is an example for the Shopgate default search. Adapt your integration to your specific search engine, search providers, and use cases.


## Testing

After the implementation of all pipelines is complete, the last step is testing. You can test with your sandbox app and the CloudFlight app.

The test cases are as follows:
- Search: Do the search suggestions appear?
- Search: Are the search results correct?
- Filter in a category view: Is the correct filter displayed?
- Filter in a search result: Is the correct filter displayed?
