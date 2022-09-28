---
sidebar_position: 4
---

# Relationships

Digital experiences are composed of many interconnected pieces of content and configuration.

Modeling content in this way helps with:

- **Flexibility** - Dividing an experience up gives you the flexibility to swap out and control individual parts of the experience. For example, repointing a "Link" to a different "Page" or adding a new "NavigationItem" to the mega menu.
- **Reuse** - Atomic pieces of content, for example, an entire page, are typically not very reusable, even though parts of the content might be. Breaking these down into smaller blocks means those blocks can be reused in other areas, other channels or by other brands.
- **Minimizing updates** - Sometimes, the same content is repeated across many locations. Using a shared piece of content allows authors to update this content once and have it apply to all locations. For example, a "BlogPost" might link to an "Author" to avoid duplicating the author's details in every blog post.
- **Independent authoring** - If a team of authors are working together to build an experience, combining smaller building blocks allows content production tasks to be divided and performed in parallel.

Amplience provides three different relationship types you can use to connect content.

## Relationships types

### Content links

Content links allow you to decompose complex content into smaller building blocks that can be independently updated and included in other content items.

Content types can have multiple content link properties that point to a child content item, creating a graph of linked content items.

![Content Link](https://cdn.media.amplience.net/i/ampproduct/content-links.png?w=200)

When the parent content item is published, linked content is automatically published as though it were part of the parent content item, guaranteeing child content items will always be available and up to date.

If multiple content items link to the same child content, changes will be reflected in all locations.

![Shared Content](https://cdn.media.amplience.net/i/ampproduct/shared-content.png?h=124)

This helps minimize how many content updates need to be made for use cases where the exact same content is repeated in many locations. If the content is not the same in every location or might diverge at a later date, it may be more suitable to duplicate the content.

Content links are commonly used for the following use cases:

- **Containers & slots** - Content objects that act as containers for other content, such as a "URL", "Page" or "Slot"
- **Blocks** - This is a design pattern where user interfaces, such as a "Page", contain an array of atomic blocks (e.g. "BannerBlock", "EditorialBlock", "GalleryBlock") that can be rearranged to create a simple layout.
- **Reusable content** - Complex content, such as a “Carousel” can be broken down into individual modules, such as “Slide” or “Banner” allowing these smaller units of content to be reused in other locations.

#### Querying linked content

When content is queried using the [Content Delivery API](/docs/apis/content-delivery/content-delivery-overview#depth), you can choose to retrieve all of the linked content, linked content up to a specific depth or just the parent content item.

### Content references

Content references allow you to reference the id of another content item without including the content of that item.

Content types can have multiple content reference properties that point to a child content item, creating a graph of weakly linked content items.

![Content Reference](https://cdn.media.amplience.net/i/ampproduct/content-references.png?w=200)

Publishing the parent content item will not automatically publish the referenced child items; therefore, the child content items may be unavailable.

Content references are commonly used for the following use cases:

- **Hyperlinking** - When one part of an experience needs to hyperlink to another, it is desirable to use a content reference so that publishing a page does not automatically publish every hyperlinked page.

### Content hierarchies

Content hierarchies provide an alternative way to model hierarchical data structures, such as navigation menus or page hierarchies.

Unlike content links, each child points to a single parent node rather than the parent pointing to child nodes, allowing each node to be updated and published independently.

![Content Reference](https://cdn.media.amplience.net/i/ampproduct/hierarchy.png?w=200)

Each node in the hierarchy is an individual content item.

You can control which content types can be part of a hierarchy using the [hierarchy trait](/docs/schema-reference/traits#hierarchy-trait). You can also control ordering of nodes using the [sortable trait](/docs/schema-reference/traits#sortable-trait).

Content hierarchies are commonly used for the following use cases:

- **Navigation menus** - Navigation menus are typically a hierarchical data structure where links have a parent link which helps inform the user interface. Modeling this as a set of independent nodes allows authors to schedule modifications (add, remove, move, update) in isolation which is beneficial for larger applications and distributed content teams.
- **Page Tree** - Websites can choose between having a flat page structure or a hierarchical page structure where each page has a parent page. This facilitates UX patterns such as breadcrumbs and can help with menus and sitemap generation. Content Hierarchies is well suited for this use case because each page should be independent.
- **Taxonomies** - Taxonomies are used to classify objects and consist of a set of terms that are typically organized into groups. Examples of this include product categories, personalization dimensions or tags. These types of structures can be modelled using a content hierarchy.

#### Querying content hierarchies

Content items inside a content hierarchy contain extra built-in properties to help your application interpret the structure.

This includes the id of its parent node `_meta.hierarchy.parentId` and a Boolean to indicate if the node is the root node `_meta.hierarchy.root`.

You can retrieve the child nodes for a specific node by querying the [Content Delivery API](/docs/apis/content-delivery/filter-api#listing-children-of-a-hierarchy-node) by parentId.

## Related pages

[Data types: content relationships](/docs/schema-reference/data-types#content-relationships)

[Schema examples: content relationships](/docs/schema-reference/schema-examples/core-concepts/combine-schemas)

[Traits](/docs/schema-reference/traits)

[Content Delivery API](/docs/apis/content-delivery/content-delivery-overview)

[Hierarchies](/docs/dev-tools/guides-tutorials/hierarchies)

[Filter API](/docs/apis/content-delivery/filter-api)
