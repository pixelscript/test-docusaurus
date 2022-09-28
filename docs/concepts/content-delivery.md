---
sidebar_position: 3
---

# Content delivery

A Headless CMS can be thought of as a specialized database. It has a data model ([Content Types](/docs/concepts/content-types)), it contains data (content objects), and there are APIs to retrieve and query the data called **[Content Delivery APIs](/docs/apis/content-delivery/)**.

These APIs provide a read-only, high throughput and low latency way for your applications and/or backends to fetch objects from the CMS.

## High throughput, low latency

Amplience Content Delivery APIs work differently from other Content Management Systems to ensure they are fast at any scale.

Traditional relational databases are commonly used in Content Management Systems but are not designed for scale. In these databases, it is very easy to write a bad query (a query that won’t scale) which results in unpredictable performance that slows down your application.

To avoid this, we don't provide a one size fits all query engine, but instead provide a set of easy-to-use query capabilities based on NoSQL principles, making it impossible for you to write a bad query accidentally.

## Querying for content objects

The Content Delivery APIs return content objects, which is the structured data entered by users when creating a content item.

Content objects are returned as JSON and will contain the properties you defined in the content type as well as some useful metadata in a reserved property called `_meta`.

Management information, such as workflow and organization information is stored as part of the content item instead of the content object so it can remain private.

### Delivery Id

Every content object has a unique `deliveryId` that can be used to fetch and refetch one or many content objects from the Content Delivery APIs.

The `deliveryId` can be thought of as a primary key, which is automatically generated and cannot be changed.

Fetching by id is suitable for use cases where your application already knows the `deliveryId` ahead of time. Examples of this include:

- **Integration between systems** - Sometimes, it is necessary to reference specific Content Objects from inside another system, such as an e-commerce platform or personalization engine.
- **Lazy loading** - To improve efficiency, your application may delay loading some of the related Content Objects until they are required.
- **Webhook applications** - Webhooks notify your application about changes to specific resources. Changes related to content include the deliveryId which you can use to query the Content Delivery API.

### Delivery key

Delivery keys provide a more convenient way to look up a content object using a custom value.

Each content object has a `deliveryKey` property that can be set at any time to a custom text value.

You can constrain the format of the `deliveryKey` in the content type as well as configure how it is displayed in the content form like any other property.

Fetching by `deliveryKey`is useful when you need to find a content object associated with something in your application or business domain. Examples of this include:

- **URL** - When building a content-managed website, it is typical to have a content type representing a URL or page. The delivery key of these objects can be set to the URL (e.g. "help/size-guide") such that the application can query the Content Delivery APIs to fetch a page for the requested URL.

- **Named slots** - This is a design pattern where placeholder areas are created inside a webpage that will be populated by a content object with a specific name / deliveryKey (e.g. "homepage-hero-slot").

- **Enriching resources** - You may have a resource (e.g. "Product Category" or "Store") that already exists in another system, but you wish to enrich the resource with additional CMS content. In this scenario, a content type can be created that captures the additional data and the `deliveryKey` can be set to include the resource id (e.g. "store/1234").

### Linked content

Content objects can contain properties that [link](/docs/concepts/relationships) to other content objects.

These linked content objects can be automatically retrieved by the Content Delivery API, avoiding the need to make additional API requests. You can choose to retrieve just the root, the entire tree of linked content, or specify a maximum depth to retrieve.

By using this capability, your application only needs to look up the initial entry point objects (e.g. "slot" by name, "page" by URL etc), while all of the linked content is automatically returned.

Automatically fetching linked content is helpful for use cases where you need the related content. Examples of this include:

- **Containers & slots** - Content objects that act as containers for other content, such as a "URL", "Page" or "Slot" are often looked up with the intention of loading and displaying the content inside that container.
- **Modular content** - This is a design pattern where complex content is composed of several smaller pieces of content, which helps improve reuse. Typically, your application will need the entire tree of content in order to display modular content.

### Filter properties

Filter properties are designated properties inside your content type that you can match against when retrieving a list of content objects from the Content Delivery API.

By default, you can filter by the content type property (`/_meta/schema`) to find every content object of a particular type.

Additionally, you can define up to 5 custom filters per content type using the [filterable trait](/docs/schema-reference/traits#filterable-trait). Each filter can target one or multiple properties, allowing for compound "AND" matches.

This capability is suitable for use cases where you need to retrieve a list of content objects filtered using simple criteria. Examples of this include:

- **Sitemap / SSG** - When building a website sitemap or using a static generator, you may need to retrieve a list of pages. Using the built-in content type filter, you can find all content objects of type page.

```json
{
  "filterBy": [
    {
      "path": "/_meta/schema",
      "value": "https://example.com/page.json"
    }
  ]
}
```

- **Blog** - In a blog application, you may wish to provide simple filtering such as filtering by category or filtering by author. Custom filters can be created for each of these properties allowing your application to query the CMS to retrieve all blog posts of a specific category or all blog posts by a specific author.

```json
{
  "filterBy": [
    {
      "path": "/_meta/schema",
      "value": "https://example.com/blog-post.json"
    },
    {
      "path": "/category",
      "value": "buying-guide"
    }
  ]
}
```

Filtering follows NoSQL principles and as such, is not suitable for every use case. For more complex querying, using a [search index](/docs/integrations/search) is the optimal choice. If your use case requires the following, you should use search over filtering:

- **Natural language search** - Allowing users to search using everyday language.
- **Faceted search** - Allowing users to narrow results by applying multiple grouped filters.
- **Complex criteria search** - Partial matches, regex matches, range matches, expressions etc.
- **Offset pagination** - Filtering uses cursor-based pagination, which is optimal for infinite scroll UX patterns. Offset pagination instead uses fixed pages to navigate data.

### Sort properties

Sort properties are designated properties inside your content type that you can use to sort results when retrieving a list of content objects from the Content Delivery API.

You can define up to 3 custom sorts per content type using the [sortable trait](/docs/schema-reference/traits#sortable-trait). Each sort requires a name and a list of properties to include in the sort. If multiple properties are defined in a custom sort, results will be sorted by each property in sequence.

By default, results are sorted by created date. This can be overridden by creating a custom sort with the name "default".

The sorting behavior will vary depending on the data type of the property:

| Data type | Sort behavior                                                                                                                    |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Text      | Properties will be sorted in UTF-8 byte order. Values larger than 128 characters will only be sorted by the first 128 characters |
| Number    | Properties with an Integer or Long value will be sorted in numeric order. Floating point values will be sorted as Text           |
| Boolean   | Properties will be sorted false followed by true                                                                                 |

### Localized properties

Properties inside a content type can be localized, meaning they contain a different value for each locale.

The Content Delivery API will return these properties as an Array containing all of the values and their associated locale-code by default.

Using the "locale" parameter, it is possible to specify a preferred locale to avoid fetching extra data. The content object is rewritten to replace localized properties with a single value that matches the preferred locale or null if no match was found.

The matching can be strict, or you can use wildcards and fallbacks to increase the likelihood of finding a match.

- **Exact match** - `locale=fr-FR`
- **Partial match** - `locale=en-*`
- **Fallback match** - `locale=fr-FR,fr-*,en-US,en-*`

## Related pages

[Content Delivery API](/docs/apis/content-delivery)

[Content Delivery SDK](https://github.com/amplience/dc-delivery-sdk-js)

[Filterable Trait](/docs/schema-reference/traits/#filterable-trait)

[Sortable Trait](/docs/schema-reference/traits/#sortable-trait)

[Search](/docs/integrations/search)

[Schema examples](/docs/schema-reference/schema-examples)
