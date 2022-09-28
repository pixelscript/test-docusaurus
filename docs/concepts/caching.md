---
sidebar_position: 8
---

# Caching

Our dynamic commerce experience platform supports high performance customer journeys through the Dynamic Content
and Dynamic Media products. They both use Content Delivery Networks (CDNs). Understanding our caches will help to design
successful high performance applications.

## Dynamic Content cache

Headless CMS empowers developers to build any type of app, but different architectures have different needs.

With this in mind, we have provided two versions of the Content Delivery APIs, one cached and one uncached. We call the
uncached one 'Fresh'.

Many apps require content to be available globally. The job of a CDN is to make sure that content can be delivered
quickly, no matter where content is requested from and no matter how many requests are being made. To do this, it has to
make copies of the content and place it close to where it might be needed. Our CDN infrastructure has many caches
globally.

![Our global CDN infrastructure](https://cdn.media.amplience.net/i/ampproduct/concepts-cdncache-lm-v3?w=1880&fmt=png&#gh-light-mode-only 'Our global CDN infrastructure')
![Our global CDN infrastructure](https://cdn.media.amplience.net/i/ampproduct/concepts-cdncache-dm-v3?w=1880&fmt=png&#gh-dark-mode-only 'Our global CDN infrastructure')

Our CDN based APIs provide fast global content delivery at high volume. These are the APIs to use for most applications.
We deliver our content from origins that are globally replicated. All customer requests are automatically routed to
the nearest POP and the nearest origin.

:::info

The cached API (_cdn.content.amplience.net_) provides cached data (~5 minutes), unlimited throughput, the lowest
possible latency and 99.99% availability.

:::

### Content cache TTL

CDN caches keep copies of content. When content changes, eventually the copies in the cache are updated. The time
in which the cached copy can be out of date is called the TTL (Time To Live). We operate our CDNs with a short a TTL as
we can so that we keep content as fresh as possible.

### Content cache updates

When the TTL has elapsed, the next request to a cache will return the currently cached copy. In the background, the
cache will then check and update to the latest copy if needed. This means that the request won't need to incur the time
cost of waiting for the latest copy. This is called stale-while-revalidate, meaning the cache will only serve stale
content while it updates to the latest copy. This optimises for speed.

### Fresh Content API

A good example of an application that should use our Fresh API is a static site generator. SSGs are typically built
infrequently by a single build process. When the SSG builds, it is essential that the latest copy of content is
retrieved. This combination of low-volume and requirement for uncached content suits our Fresh API.

:::info

The fresh API (_fresh.content.amplience.net_) provides up-to-date data, lower rate-limited throughput, low latency and > 99.9% availability.

:::

Note that the Fresh API requires the use of an API key.

### Recommendations

<details>
<summary>Recommendations by Architecture</summary>

| Architecture                           | Content Delivery API |
| -------------------------------------- | -------------------- |
| Client Side App (iOS/Android/SPA/JS)   | Cached               |
| Isomorphic PWA                         | Cached               |
| Server Side Rendered PWA (SSR)         | Cached               |
| Server Side Rendered PWA (SSR) + Cache | Cached or Fresh      |
| Static Site Generator                  | Fresh                |
| Server Side API                        | Cached               |
| Server Side API + Cache                | Cached or Fresh      |

</details>

## Dynamic Media cache

Media is used differently to content objects. Here are ways in which media is different:

- Usually it is a customer's browser that retrieves media directly, applying the transformations it needs dynamically.
- One image may be used in many hundreds of different ways, each one tailored to the channel and customer experience.
- Media can be layered with additional content.
- Media can be personalized, especially with our monogramming feature.

Our Dynamic Media caching infrastructure is tailored for high performance media delivery. Amplience maintains this high
performance by leveraging three caches:

- **Browser Cache**: for the fastest possible retrieval by the customer.
- **Mid-Tier Cache**: a purgeable request cache that provides low-latency retrieval.
- **Edge CDN Cache**: geographically distributed cache layer, close to the customer.

### Browser cache

The fastest media retrieval is for the browser to use the locally stored copy. Our delivery configurations allow you
to control what directives are given to the browser cache. Striking a balance between performance and freshness is
important, so we provide sensible defaults.

### Edge CDN cache

The Amplience CDN is a global network of POPs that cache media as close to the requestor as possible. This is a
read-through request cache that has a TTL that you can configure.

### Mid-tier cache

Our Dynamic Media APIs are feature-rich, requiring significant compute resource to produce fast media responses. Our
mid-tier cache sits in front of this capability and provides low-latency retrieval of assets for our edge CDN. When
assets are published, this tier is automatically purged so that the edge CDN can always retrieve the latest copy.

:::info

Our publish process automatically purges the mid-tier cache, so there's no configuration required.

:::
