---
sidebar_position: 11
---

# Personas

## About personas

To perform a given task in Dynamic Content, for example creating and editing content, or creating and scheduling editions, a user must have the appropriate permissions, as well as the required access to the hubs and repositories in which these tasks are performed.

The roles of different types of users within a team are represented by a standard set of personas: content producer, planner, developer, admin and a read only user. Each of your users must be allocated one of these personas at the beginning of your project, or when new users are added. A persona has a set of permissions attached to it, as explained in more detail below.

As explained on the [account structure](/docs/concepts/account-structure) page, all users have read only access for all content repositories within a hub.

![Content producer](https://cdn.media.amplience.net/i/ampproduct/avatar-marketer?w=120&fmt=png 'Content producer')

## Content producer

A user with the content producer persona can create, edit and archive content items. They also have permission to create, edit and delete folders.
Note that content producers do not have permission to publish content.

**You need to specify:**

- The hubs that the user has access to.
- In which content repositories the user can create content. If a content producer does not have permission to create content in a particular repository, they will have read only access.

![Users with the content producer persona can create, edit and archive content items](https://cdn.media.amplience.net/i/ampproduct/personas-01?w=1880&fmt=png 'Users with the content producer persona can create, edit and archive content items.')

![Planner](https://cdn.media.amplience.net/i/ampproduct/avatar-digitalleader?w=120&fmt=png 'Planner')

## Planner

Planners have permission to perform all the tasks of a content producer, but can also publish content. In addition planners can create, edit and delete events and editions as well as scheduling editions.

**You need to specify:**

- On which hubs a planning user has permission to create, edit and delete events and editions.
- The repositories in which they can create content.

![The planner persona includes all the permissions of a content producer as well as the ability to publish content and work with events and editions](https://cdn.media.amplience.net/i/ampproduct/personas-02?w=1880&fmt=png 'The planner persona includes all the permissions of a content producer as well as the ability to publish content and work with events and editions.')

![Developer](https://cdn.media.amplience.net/i/ampproduct/avatar-developer?w=120&fmt=png 'Developer')

## Developer

Users with a developer persona have all the permissions of a planner, but can also create, edit and archive slots.

The developer persona also allows access to the features in the Developer tab to:

- Register a content type with a hub and enable a content type with a repo.
- View, edit and delete webhooks
- Archive content types and content type schemas
- View integrations
- View, create and edit Salesforce Commerce Cloud (SFCC) integrations
- Register and manage extensions
- Create, read, edit and delete search indexes (on hubs which have [Dynamic Content search](/docs/integrations/search) enabled)

**You need to specify:**

- In which slot repositories the user can create, edit and archive slots.
- The hubs on which this user has developer access

![Users with a developer persona can create, edit and archive slots and access the features in the development tab](https://cdn.media.amplience.net/i/ampproduct/personas-03?w=1880&fmt=png 'Users with a developer persona can create, edit and archive slots and access the features in the development tab.')

![Customer admin](https://cdn.media.amplience.net/i/ampproduct/avatar-techleader?w=120&fmt=png 'Customer admin')

## Customer admin

A user with the customer admin persona has permission to perform the role of content producers, planners and developers, but in addition can also:

- Edit workflow states for a hub

**You need to specify**: the hubs and repositories that the user needs admin access to.

To create repositories please raise a support request with Amplience support.

**Note:** requests to make changes to user permissions should be directed to Amplience support or, during your project implementation, to your Customer Success Manager.

## Read only

A user with the read only persona can view content, events and editions, but not create or edit content, events or editions.

**You need to specify:** The hubs to which this user has read only access.

:::note

It is not possible to mix permissions between personas. For example, a content producer cannot be granted some but not all of the privileges of a planner. You must choose one of the defined personas for a user, even if it means giving the user slightly more privileges than required.

:::

## Related pages

[Hubs and repositories](/docs/concepts/account-structure)
