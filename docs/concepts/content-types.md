---
sidebar_position: 2
---

# Content types

A content type is a blueprint that describes a specific data structure users can create and manage inside the CMS, such as a page, banner, blog post etc.

The content types you create will depend on the type of experience you are making. Most applications have multiple content types, referred to in aggregate as a "content model".

You can use content types to represent any concept that business users may need to control, including non-visual elements such as configuration.

![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-contenttypes-lm-v3?w=1880&fmt=png&#gh-light-mode-only 'Content types')
![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-contenttypes-dm-v3?w=1880&fmt=png&#gh-dark-mode-only 'Content types')

Typically, you will perform an exercise called ["content modelling"](/docs/concepts/content-modeling), where requirements and wireframes are translated into a content model.

## Anatomy of a content type

Content types contain a few different elements:

![Content Type Structure](https://cdn.media.amplience.net/i/ampproduct/content-model-lm-v3?w=600&fmt=png&#gh-light-mode-only 'Content Type Structure')
![Content Type Structure](https://cdn.media.amplience.net/i/ampproduct/content-model-dm-v3?w=600&fmt=png&#gh-dark-mode-only 'Content Type Structure')

- **Schema** - This is where the data structure is defined, using a powerful open standard called [JSON Schema](https://json-schema.org/).
- **Properties** - These are the fields users will enter when creating content. This data will be available to your application to retrieve and use to render an experience.
- **Configuration** - Configures how the content type should appear in the CMS interface.

## Schema

A schema defines the data model for a content type.

We think CMS tools should be flexible enough to model your data rather than making you model your data and code to fit the CMS. To do this, we use a powerful open standard called [JSON Schema](https://json-schema.org/) to give you as much flexibility as possible to model precisely the data you want.

When users select a content type and begin creating content, the CMS interprets the schema and automatically generates a simple-to-use authoring interface that will produce data that matches the structure you have defined.

### Example schema

JSON schema describes the format of JSON structures using a set of keywords that you can mix and match.

Imagine you are building a blog application and wanted to create a blog post content type with the following structure:

```json
{
  "title": "...",
  "author": "...",
  "description": "..."
}
```

To define this structure, we can start with the `type` keyword. In this case, the structure is an `object`.

```json
{
  "type": "object"
}
```

Next, we can use the `properties` keyword to define the individual fields. Notice how each property is also defined using a schema. You can use all the same keywords and nest schema recursively to create complex structures.

```json
{
  "type": "object",
  //highlight-start
  "properties": {
    "title": { "type": "string" },
    "author": { "type": "string" },
    "description": { "type": "string" }
  }
  //highlight-end
}
```

To prevent our blog application from receiving bad data, we can also add validation keywords such as `required` or `maxLength`.

```json
{
  "type": "object",
  "properties": {
    //highlight-next-line
    "title": { "type": "string", "maxLength": 50 },
    "author": { "type": "string" },
    "description": { "type": "string" }
  },
  //highlight-next-line
  "required": ["title", "author", "description"]
}
```

Finally, we just need to add a little bit of boilerplate to complete the schema.

```json
{
  //highlight-start
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://example.com/blog-post.json",
  "allOf": [
    { "$ref": "http://bigcontent.io/cms/schema/v1/core#/definitions/content" }
  ],
  //highlight-end
  "type": "object",
  "properties": {
    "title": { "type": "string", "maxLength": 50 },
    "author": { "type": "string" },
    "description": { "type": "string" }
  },
  "required": ["title", "author", "description"]
}
```

- **$schema** - The `$schema` keyword tells the system what version of JSON Schema we are using.
- **$id** - The `$id` keyword gives the schema a unique id so it can be referenced. The format of this is a URI but you can use any value you want, it does not need to resolve.
- **allOf** - This is a [mixin](#mixins) that tells the system this schema is a content type. It adds some extra metadata properties to your content type that the CMS will populate automatically.

You now have a schema that could be registered as a content type. If you would like to learn more about JSON schema, check out the [Schema reference](../schema-reference/).

## Schema data model

### Properties

Properties are the individual fields users will be asked to populate when creating content.

Based on your requirements, these properties are defined inside the schema using the `properties` keyword.

Each property has a name, which is how it will appear in the JSON output, an optional `title`, which is how it will appear in the authoring interface and a schema that defines the structure.

```json
{
  "properties": {
    "author": { "title": "Author", "type": "string" }
  }
}
```

You can choose from a wide range of built-in data types to ensure the data is in the correct format for your application.

| Data type            | Description                                                                                                               |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Text                 | A plain text value with full UTF-8 unicode character support                                                              |
| Rich text            | A formatted rich text value (Markdown)                                                                                    |
| Number               | An integer or decimal values, equivalent to JavaScript Number                                                             |
| Integer              | An integer value                                                                                                          |
| Boolean              | A true or false value                                                                                                     |
| Date/time            | A date, time or date-time value                                                                                           |
| Color                | An RGB or RGBA color                                                                                                      |
| Image                | A reference to an Image file hosted inside Amplience                                                                      |
| Video                | A reference to a Video file hosted inside Amplience                                                                       |
| Object               | A nested inline object with properties                                                                                    |
| Array                | An Array, where each entry in the Array an be any data type                                                               |
| Content relationship | A reference to other Content stored inside the CMS. There are multiple types of relationship to suit different use cases. |

More complex structures are modelled by creating nested objects with their own `properties`.

```json
{
  "properties": {
    "author": {
      "title": "Author",
      "type": "object",
      "properties": {
        "firstName": { "title": "First Name", "type": "string" },
        "lastName": { "title": "Last Name", "type": "string" }
      }
    }
  }
}
```

### Arrays

The array data type is used to model properties that contain multiple values.

Arrays can be created for any data type, e.g. Arrays of Images, Videos, Strings, Objects, References to other Content etc.

The `items` keyword is used to define the structure of each item in the Array.

For example, a String Array would be defined as:

```json
{
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

A more complex Array of objects would be defined as:

```json
{
  "type": "array",
  "title": "Authors",
  "items": {
    "type": "object",
    "properties": {
      "firstName": { "title": "First Name", "type": "string" },
      "lastName": { "title": "Last Name", "type": "string" }
    }
  }
}
```

### Validation

Users can update content at any time and it is important that updates don't break your application.

To prevent invalid data from reaching your application, we provide a range of validation options you can use to restrict the data that users can be enter.

| Validation type                                                              | Description                                                                                                                                                                                          |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Enumerated values](/docs/schema-reference/validation#enumerated-values)     | Restricts the value to a fixed set of possible values. Properties using this validation will display as a dropdown.<br />`{"enum": ["red", "blue", "green"]}` `{"enum": [1,2,3]}`                    |
| [Constant values](/docs/schema-reference/validation#constant-values)         | Restricts the value to a constant value. Users will be unable to change the value in the authoring interface.<br />`{"const": "BannerComponent"}`                                                    |
| [Regular expression](/docs/schema-reference/validation#regular-expression)   | Validates the format of text values matches a custom regular expression<br />`{"pattern": "[a-z]+"}`                                                                                                 |
| [Text minimum length](/docs/schema-reference/validation#text-minimum-length) | Validates the minimum length of a text value<br />`{"minLength": 1}`                                                                                                                                 |
| [Text maximum length](/docs/schema-reference/validation#text-maximum-length) | Validates the maximum length of a text value<br />`{"maxLength": 50}`                                                                                                                                |
| [Text format](/docs/schema-reference/validation#text-format)                 | Validates the format of text values matches the specified built-in format<br />`{"format": "date"}` see [Schema reference](/docs/schema-reference/validation#text-format) for a full list of formats |
| [Number minimum value](/docs/schema-reference/validation#minimum-value)      | Validates that the value entered is more than or equal to the minimum value.<br />`{"minimum": 0}` or `{"exclusiveMinimum": 0}` for just more than                                                   |
| [Number maximum value](/docs/schema-reference/validation#maximum-value)      | Validates that the value entered is less than or equal to maximum value.<br />`{"maximum": 10}` or `{"exclusiveMaximum": 0}` for just less than                                                      |
| [Number multiple](/docs/schema-reference/validation#multiple)                | Validates that the value entered is a multiple of the multipleOf value<br />`{"multipleOf": 2}`                                                                                                      |
| [Required properties](/docs/schema-reference/validation#required-properties) | Validates that the specified properties must be populated.<br />`{"properties": {"name": {"type": "string"}}, "required": ["name"]}`                                                                 |
| [Array minimum items](/docs/schema-reference/validation#array-minimum-items) | Validates that the Array value contains at least the minimum number of items<br />`{"minItems": 1}`                                                                                                  |
| [Array maximum items](/docs/schema-reference/validation#array-maximum-items) | Validates that the Array value does not contain more than the maximum number of items<br />`{"maxItems": 1}`                                                                                         |
| [Array unique items](/docs/schema-reference/validation#array-unique-items)   | Validates that every item in the Array is unique<br />`{"uniqueItems": true}`                                                                                                                        |

### Localization

If you need to support multiple locales, you can create [localized properties](/docs/dev-tools/guides-tutorials/localization) inside your schema.

You can choose which properties should be localized and you can use any data type or structure you want, not just text.

The authoring interface will display a value for each locale that has been configured on the hub.

![Authoring localized properties](https://cdn.media.amplience.net/i/ampproduct/localized-content-3)

Behind the scenes, the system will store these properties as an Array. When requesting content from the [Content Delivery API](/docs/apis/content-delivery/content-delivery-overview#localized-properties), you can return all localized values or ask the API to select the most appropriate value by providing a fallback list of locale codes.

Amplience also provides a second type of localization you can use alongside or instead of localized properties called [Item level localization](/docs/user-guides/produce-content/localize#content-item-localization).

In this approach, each locale has its own distinct content item, which means they can be worked on and published separately. This is helpful for situations where each locale has independent authors.

![Item level localization](https://i8.amplience.net/i/amplience/items%20small?&$retina-desktop$&fmt=webp&qlt=100)

### Mixins

Code often reuses the same data structures in multiple places, and content types are no different.

Instead of duplicating these data structures, which quickly gets out of sync, you can define them once and then reference them using the `$ref` keyword.

You can reference any part of any schema by providing the location, a combination of the schema id and a pointer that indicates the path to the structure.

```json
{
  "properties": {
    "seo": { "$ref": "https://example.com/mixins.json#/definitions/seo" }
  }
}
```

In addition, there is also a special type of schema called a "partial schema", which are not intended to be used as a content type but instead act as a library of data structures you can reference.

The referenced properties will appear in the authoring UI and save data inline like any other property.

As updates are made to the shared data structures, these are automatically reflected in every content type that references the structure.

### Traits

[Traits](/docs/schema-reference/traits) are special features you can switch on for a given content type to enhance its functionality.

| Trait                                                              | Description                                                  |
| ------------------------------------------------------------------ | ------------------------------------------------------------ |
| [Filterable Trait](/docs/schema-reference/traits#filterable-trait) | Enables content to be filtered by a set of custom properties |
| [Sortable Trait](/docs/schema-reference/traits#sortable-trait)     | Enables content to be sorted by a set of custom properties   |
| [Hierarchy Trait](/docs/schema-reference/traits#hierarchy-trait)   | Enables content to be managed as a hierarchical tree         |

## Configuration

A content type's configuration determines how it will appear inside the CMS interface. Setting these up dramatically improves the experience for authors and helps them be more productive.

### Icons

Content types can be assigned an icon (built-in or custom) to help authors visually find the content type they want to use.

![Content Type Icons](https://cdn.media.amplience.net/i/ampproduct/content-type-icon-4?w=1880&fmt=png&crop=0,0,100%,450)

### Cards

Cards act as a thumbnail for a piece of content, making it much easier to spot when browsing folders or search results.

You can configure a content type to use a built-in card or create your own.

Built-in cards require you to choose which properties inside your schema should be displayed in the thumbnail; different cards support different data types (e.g. images, arrays, text).

![Content Thumbnail Photo Card](https://cdn.media.amplience.net/i/ampproduct/summary-photo-2?w=250) ![Content Thumbnail Text Card](https://cdn.media.amplience.net/i/ampproduct/text-card-2?w=250) ![Content Thumbnail Gallery Card](https://cdn.media.amplience.net/i/ampproduct/gallery-card-3?w=250)

If you want to create a custom card, these are implemented as a lightweight web page loaded into the CMS interface every time a thumbnail is displayed. Information about the content item will be passed in as parameters.

### Visualization

Visualizations let authors preview how content will look inside your application.

This works by embedding your app in the authoring interface side by side. The CMS will provide information to your app so it knows what content to display and where to load it from.

![Visualization](https://cdn.media.amplience.net/i/ampproduct/view-visualization-1?w=1880&fmt=png)

When you set up a content type, you can provide a list of apps the CMS should embed as visualizations. Typically, the same apps will be used across all content types but there may also be content types designed for specific apps (e.g. Android/iOS apps).

### Repositories

Content types are enabled or disabled per content repository, giving you the flexibility to create groupings of content types for different situations.

For example, if you created repositories for each app (website, iOS, Android) you can prevent mobile-specific content types from being used on the website by not enabling them on the website repository.

## Related pages

[Content modeling](/docs/concepts/content-modeling)

[Schema reference](/docs/schema-reference)

[Schema examples](/docs/schema-reference/schema-examples)

[Built-in cards](/docs/dev-tools/guides-tutorials/content-types)

[Developing custom cards](/docs/dev-tools/guides-tutorials/content-types)

[Developing visualizations](/docs/dev-tools/guides-tutorials/visualizations)

[Registering content types](/docs/dev-tools/guides-tutorials/content-types)
