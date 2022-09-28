---
sidebar_position: 10
keywords: [organizations, organizations, hubs, repositories, personas]
---

# Account structure

When you are deciding how to set up Dynamic Content for your organisation, one of the issues to consider is how to organise hubs and repositories. Hubs are the top level space within which content is organised and scheduled, and these hubs contain repositories in which the content and slots are stored.

Depending on your requirements and how you share content between brands, you may choose to have more than one hub, or use one hub and multiple repositories to contain the content for each brand. On this page we'll explain the various options.

For more information about the roles of different types of users and what the permissions they are granted, see the [personas](/docs/concepts/permissions) page.

## Hubs

Hubs are organised around a set of design principles that you can use to help decide whether to have a single or many hubs.

The image below shows an account with multiple hubs (1) and the "Amplience Product Hub" selected. This hub contains several repositories (2 in the image below).

!["A Dynamic Content account with multiple hubs. The selected hub has multiple repositories.](https://cdn.media.amplience.net/i/ampproduct/hubs-and-repositories-01?w=1880 'A Dynamic Content account with multiple hubs. The selected hub has multiple repositories.')

### Hub characteristics

- Permissions are set at the hub level. All users of a hub can at least view all of the content within the repositories inside that hub.
- Content cannot be shared across hubs.
- However, content can be shared and linked to across repositories within the same hub. So you can create a content item in one repository and include content stored in another.
- Events and editions are scheduled within a single hub. So if you want an overall view of the planning calendar across many brands, then you may wish to consider a single hub. However, in some cases you may want to keep the calendars separate.
- Many settings, such as the publishing endpoint (the subdomain to which your content is published) are set at a hub level. Multiple hubs may publish content to the same endpoint.

## Repositories

- Although a user can view content in all repositories within a single hub, their ability to create content may be limited to certain repositories. Typically you will want your content producers to be able to create content in one or more repositories, but your planners to only be able to view the content.
- Content and slot types are registered with hubs and enabled on repositories. So you can choose which types of content can be created in each repository, or just choose to limit the number of content types that are available.

## Scenarios

Here are two scenarios which help to explain the use cases for single versus multiple hubs. For each use case we'll show the way that hubs and repositories are organised and how this effects the role of planners, content producers and developers.

### Sharing content between brands

If you have multiple brands and want to share the content across brands and possibly across channels and locales, you may choose to have one hub and several repositories.

The image below shows a possible set up of repositories all in a single hub.

![One hub for multiple brands](https://cdn.media.amplience.net/i/ampproduct/concepts-accountstructure-1hub-lm-v3?w=1880&fmt=png&#gh-light-mode-only 'One hub for multiple brands')
![One hub for multiple brands](https://cdn.media.amplience.net/i/ampproduct/concepts-accountstructure-1hub-dm-v3?w=1880&fmt=png&#gh-dark-mode-only 'One hub for multiple brands')

#### What each type of user can do

**Content producers**: can view content for both brands x and y and create content in both repositories if they are given permission to do so

**Planners**: can view the entire content planning calendar and schedule editions across both brands

**Developers**: can be given permission to create slots in both slot repositories.

If the layout of the sites or apps for both brands is very similar, then you might choose to use the same slots for each brand and store the slots in a single repository.

### Multiple hubs

If you have multiple brands and do not wish share content between them, or simply wish to keep the content entirely separate, then the multiple hub approach is one to consider.

A very simple example of this is shown below.

![One hub for each brand](https://cdn.media.amplience.net/i/ampproduct/concepts-accountstructure-2hubs-lm-v3?w=1880&fmt=png&#gh-light-mode-only 'One hub for each brand')
![One hub for each brand](https://cdn.media.amplience.net/i/ampproduct/concepts-accountstructure-2hubs-dm-v3?w=1880&fmt=png&#gh-dark-mode-only 'One hub for each brand')

#### What each type of user can do

**Content producers**: cannot share content between brands, but can be sure that content is kept separate.

**Planners**: can view the planning calendar for one brand at a time and must switch hubs to view the other brand schedule.

**Developers**: can be given permission to each hub to deploy content types and slots, but must set them up on each hub.

## Related pages

[Personas](/docs/concepts/permissions)

[Localization](/docs/user-guides/produce-content/localize)

[Repository settings](/docs/user-guides/basics/dynamic-content/settings#repository-settings)
