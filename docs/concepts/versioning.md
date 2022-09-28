---
sidebar_position: 7
---

# Versioning

Amplience automatically keeps track of changes made to content so that you can see changes over time, roll back changes and control which versions of content are available on your website or applications.

Additionally, we keep track of the links between content. A significant advantage of headless CMS is the ability to modularise and reuse content. In this case, tracking the entire collection of content is essential, not just the individual elements.

The Amplience versioning system takes linked content into account and ensures the correct versions are published to your website or application without compromising productivity.

## Versioning content

When we create content, we create content items, which have two distinct parts:

![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-versioning-lm-v3?w=1880&fmt=png&#gh-light-mode-only 'content item breakdown')
![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-versioning-dm-v3?w=1880&fmt=png&#gh-dark-mode-only 'content item breakdown')

- **content object** - This contains the content entered by users in the authoring interface that will be published to your website or application. It will include the properties you defined in the [content type](/docs/concepts/content-types).
- **content metadata** - This contains important information about the content item, such as who created it, which folder is it in, what is the workflow status, who published it last etc. This information is considered private and not published.

When we create content items, they are at version 1. Every time the content object inside the item is modified, we create a new version and increment the version number. Each item has a history of all its versions. This full history of all versions lets you view and restore from any previous version.

Other actions, such as publishing, moving items between folders, or changing a workflow status are recorded in the version history but do not create a new version, because the content remains the same.

### Version history

The version history for each content item includes the list of content versions and the associated actions that have taken place, such as publishing, changing folders, changing workflow etc.

Each entry inside the version history includes a timestamp and the user who performed the action.

![Version History](https://cdn.media.amplience.net/i/ampproduct/content-revision-history-01)

### Restoring versions

The CMS keeps a complete copy of every version of the content. You can use this information to view or restore any previous version.

Restoring a previous version creates a new version with the same content as the earlier version.

![Restoring Content Versions](https://cdn.media.amplience.net/i/ampproduct/content-revision-history-04)

## Versioning linked content

Content can contain properties that link to other content, forming what we call a content graph.

As content is edited, the items in this graph will change. New items might become part of the graph, or removed from it. Items already in the graph might have their content updated, creating a new version.

This poses a problem if you want to send your content for review or schedule it to be published in the future. If any linked items are modified in the meantime, the target audience won't see what you saw; instead, they will see a mix of your changes and someone else's changes.

Some CMS tools use "content locking" to solve this, but this prevents authors from moving on to preparing the next set of changes. Instead, Amplience has a concept called "Snapshots" that solves this problem.

### Snapshots

Snapshots record a content graph at a point in time.

When a snapshot is created for a content item, the system will find all of the linked items and record the current version numbers for the root and linked items inside the snapshot.

Snapshots can also contain an optional comment to allow the author to describe their changes.

Once an author has finished a set of changes, they can send them for review, promote to preview, publish or schedule them. These actions take a snapshot of the relevant content to use as the source of truth about what changes the author wishes to make.

![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-snapshots-lm-v3?w=1880&fmt=png&#gh-light-mode-only 'An example snapshot')
![Content types](https://cdn.media.amplience.net/i/ampproduct/concepts-snapshots-dm-v3?w=1880&fmt=png&#gh-dark-mode-only 'An example snapshot')

## Related pages

[Publishing and scheduling](/docs/concepts/publishing-scheduling)

[Preview and staging](/docs/dev-tools/guides-tutorials/virtual-staging)

[Version History](/docs/user-guides/produce-content/revisions/)

[Creating Snapshots](/docs/user-guides/schedule-content/plan/add-content-edition#tag-a-snapshot-to-an-edition-from-the-content-form)
