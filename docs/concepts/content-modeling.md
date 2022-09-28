---
sidebar_position: 1
---

# Content modeling

Content modeling is the process of translating the various types of content in your website or app into a structured set of components that can be managed in the CMS and retrieved from our APIs.

## The process of content modeling

Content modeling is best done as collaborative process that includes UX designers, developers and importantly the editorial users who will author the content.

![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-contentmodelling-lm-v3?w=1880&fmt=png&#gh-light-mode-only 'The content modeling process')
![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-contentmodelling-dm-v3?w=1880&fmt=png&#gh-dark-mode-only 'The content modeling process')

### 1. Requirements & wireframes

The first step is to define the experience you are aiming for. Wireframes are a great tool and make it easy for everybody to understand exactly what you are trying to achieve and how it all fits together. Make sure you map out all the types of content you want to create and where it should appear in your website or app. These designs will also help identify the key information you need to model in order to drive the final render.

### 2. Break it down into modules

One of the advantages of a headless approach is your content can be reused and recombined both within and across your channels. To make the most of this you need to break down your content down into modules as opposed to taking a traditional 'whole page' approach.

It is also important to think about how your content modules will relate to each other, for example a carousel might be composed from a series of promotional banners, or a navigation menu may consist of a hierarchy of linked items. If you have complex model with many relationships then a simple Entity Relationship Diagram may be helpful.

### 3. Design content types

Once you have figured out how your content breaks down into modules you need to translate these modules into content types.

For each module create a content type with properties that match your content. These properties define both the authoring interface and the structure of the data returned by the APIs.

Define validation rules if you need to ensure the data entered meets particular criteria - for instance that an image or title must be added - this gives authors and developers confidence that the experience can't be broken by publishing bad or incomplete data.

[Relationships](/docs/concepts/relationships) between content items can also be defined in your content types, different types of relationship are available according to your use case.

It's often possible to identify common 'building block' components that can be reused across different elements of your experience.

### 4. Evaluate and iterate

Don't expect to be right first time - start small and build an end-to-end example. Test your content types capture all the information required by your application in a structure that is usable for business users.

## Things to think about

Designing a content model is as much art as science - there is no one-size-fits-all approach.

### Creating an optimal authoring interface

One of the most common mistakes is designing a content model that is heavily optimised for developers without considering how it will impact the authoring experience for business users. Typically this manifests in two ways:

- An overly granular model where content types are mapped to atomic elements of the experience - e.g. a banner component with a nested button component. This results in a complex authoring experience where business users need to create and navigate between multiple linked content items - potentially adding a lot of unnecessary clicks.
- Uber configurable 'swiss-army-knife' content types that allow content components to configured in multiple ways - for example allowing multiple styling or layout options. Whilst a degree of configurability is great, too much can mean the content authoring interface is swamped with fields catering for every eventuality. It's a balance, but representing significantly different configurations as different content types can sometimes simply things for authors.

### Business workflows and productivity

As discussed above, an overly granular model can result in unnecessary complexity and add a lot of unnecessary clicks to the authoring journey.

When considering how to modularise your content it is important to consider how business users intend to manage and update content in your experiences.

Try to align your content types with units of content that mean something to authors and editors - hero banner, blog, carousel.

Consider the frequency at which different elements of your experience will be updated or changed. Align the structure of your content model so that it makes it easy to update the high frequency elements without dependencies on other less volatile items.

Think about dependencies - working with large units of content e.g. a page, can sometimes slow things down as multiple teams may end up stepping on each others toes. Smaller units such as a banner can be easier to work with as they typically have less dependencies.

### Content reuse

Reusing content can both within experiences and across different channels can be extremely useful, both in reducing effort and ensuring consistency. Be aware however that it can increase the risk of unintended consequences as changes to single module will apply everywhere that it is used.

### Content composition

A key benefit of structured content is that atomic content items can be composed together to form more complex organisms.

There are two different ways to combine content types:

#### Linked content

Linked content items are saved independently from the parent and may be shared and reused. There are three key ways to link content items, each suited to different scenarios:

- [Content links](/docs/concepts/relationships#content-links) create a hard link between parent and child, this means that when the parent is retrieved via the API any linked children are also retrieved by default. This is useful when the child items always need to be load for instance slides in a carousel. Similarly when publishing a parent item, any linked children will also be published.
- [Content references](/docs/concepts/relationships#content-references) create a soft link, meaning that when the parent is retrieved via the API, any linked children are only referenced, not automatically retrieved. This is useful when child content should only be retrieved on demand, for example a hyperlink between pages. In this case you would only want to load the linked item when the link was actually clicked. When using content references, publishing a parent item will not automatically publish referenced children.
- [Hierarchies](/docs/dev-tools/guides-tutorials/hierarchies) invert the parent child relationship, with so that child items reference their parent. This type of relationship is specifically designed to model trees of content such as navigation menus. It is possible to publish items individually or include child items when publishing a parent.

#### Inline content

Unlike linked content, [inline content](/docs/schema-reference/data-types#inline-content) is saved as part of the parent and is indivisible from it.

This is useful if the child items are never going to be reused anywhere else as it results in less content items to manage and a more efficient authoring experience.

In all cases you can specify which content types can be combined, this allows you to control the structures that can be created.

### Slots

Slots are a special type of content which allow developers to map out areas in their experiences where content can be published, including the types of content allowed in each slot. These slots then appear in the CMS interface, allowing business users to add and schedule content according to the rules defined.

When [modeling slots](/docs/dev-tools/guides-tutorials/slots#designing-your-slots), consider what areas of your experiences should have content and at what frequency this content is likely to change.

For instance a home page might be divided into a 'hero slot' and a 'body slot' if the hero image will change more frequently than the rest of the page. This allows just the hero to be updated rather than having to include the body content when a change is made.

## Related pages

[Relationships](/docs/concepts/relationships)

[Inline content](/docs/schema-reference/data-types#inline-content)

[Slots](/docs/dev-tools/guides-tutorials/slots)
