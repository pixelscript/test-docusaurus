---
sidebar_position: 6
---

# Publishing and scheduling

Dynamic Content manages content as content items. Content items have two distinct parts that help with managing content ready for publishing.

The first part is the _content object_. This is the JSON data that represents the content as entered by an author according to the structure and validation defined by your schema - for example a banner or an article.

The second is _content metadata_. This records important information such as who created it, the current version and its journey through a workflow.

Publishing is a process that works with content items and takes the _content objects_ from the Dynamic Content back-office and places them in our delivery systems, ready to be consumed by applications via our delivery APIs.

![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-publishing-lm-v3?w=1880&fmt=png&#gh-light-mode-only 'The publishing process')
![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-publishing-dm-v3?w=1880&fmt=png&#gh-dark-mode-only 'The publishing process')

This separation of back-office from delivery gives the freedom to manage content according to your business processes. We provide features such as versioning and scheduling to help with this.

## Versioning

Every time the content object is modified we create a new version of the content item. The version history is recorded, and you can restore an item from any of its previous versions.

Moving items between folders, or changing a workflow status doesn't bump the version. That is because these changes don't affect the content object. We have this distinction so that it is clear what changes will actually make a difference to your applications when they are published.

## Content graphs

Content items can contain content-links to other content items, forming a content graph. When a content item is published, any linked content items are published automatically.

As we edit content, the items in this graph can change. New items might become part of the graph, or removed from it. Choosing what content to publish means knowing the shape of the content graph and the versions of all the content items it contains. Snapshots do exactly this.

## Snapshots

Snapshots are the behind-the-scenes magic that helps you preview, validate and schedule items so that the right content goes live at the right time.

A snapshot captures the versions of all content in a content graph at a given point in time. Snapshots are immutable: once a snapshot is taken, it doesn't change.

Snapshots are automatically taken at key transition points in the content production workflow, for example when content is previewed, published or added to an edition.

Together with versions, snapshots mean that we don't ever need to use content locking to prevent unwanted changes being introduced. The content grpah scheduled, published or previewed will be at the versions intended irrespective of any subsequent changes to any of the content items it contains. This really helps in maximising productivity during content production in teams, especially when working with more complex content items.

## Publishing

Publishing takes content and makes it available in delivery. Whenever we publish items, we want to make sure that all of its linked items are also published. The process uses snapshots to do this, making a content graph with all links and their links. Once the snapshots exists, there is a known consistent collection of content. The publishing process then uses this snapshot to copy content objects into delivery.

Publishing is a highly reliable process. It does all of the complex work up-front to prepare and validate the changes. This makes sure that when the publish time arrives, content is reliably and quickly placed into delivery systems. Nobody wants to stay up until midnight to check if content was published successfully.

Content can be published as-needed, at any time, directly from the content item. Alternatively it can be scheduled to go live at a specific time in the future.

## Scheduled publishing

_Events_ and _Editions_ allow you to schedule content updates in advance.

Editions define _when_ and (optionally) _where_ content should be published. Multiple content items can be added to an edition, either directly or in slots. Slots define areas of your experience where business users can manage content.

The edition start-time defines when the content and slots in that edition will be published. Content is never un-published - it's safer that way - but the edition end-time can be used by your application to make content inactive.

When content is added to an edition, a snapshot of the content is taken - this ensures the intended version of content will be published irrespective of any changes to the content between scheduling and publishing.

Editions are organised into _Events_. Events allow related updates to be grouped together, for example they can be used to represent campaigns, projects or updates to a particular channel.

Point-in-time preview allows you to look into the future to see how your scheduled content will appear on a given date across all your experiences, taking in to account anything else that's scheduled.
