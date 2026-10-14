---
layout: post
title: "Scaling Internal Links: Hub-and-Spoke on Next.js"
tags: [nextjs, seo, architecture, linking]
---

Hey everyone,

I wanted to share a bit about how I’m handling internal linking across my network of small content sites. As a solo founder, efficiency is key, and I needed a way to manage SEO value flow without manually updating hundreds of links every time I publish something new or move a page.

The approach I've settled on is a hub-and-spoke model, implemented across multiple Next.js sites. Each site acts as a spoke for certain topics, and then there are designated 'hub' pages or even entire sites that aggregate content around broader themes. The key is automation and a consistent linking strategy.

When I publish a new article on a site like [gotfo.com](https://gotfo.com) (my gardening site), it automatically builds links to relevant hub pages within gotfo.com, but also, critically, to related hub pages or even specific articles on other sites in the network. For example, a post about 'starting seeds indoors' on gotfo.com might link to a 'DIY grow tent' guide on [afixu.com](https://afixu.com) (my home improvement site), and vice versa. This cross-site linking is done programmatically during the build process, using a shared data layer that understands the topical relationships between content.

This isn't about link schemes, but about genuinely connecting relevant content for users and search engines. It ensures that new content gets immediate internal link equity and that older, authoritative content continues to pass value. It also means I don't have to manually go back and edit old posts to add new links, which saves a huge amount of time.

Happy to elaborate on the technical setup if anyone has questions about this specific part.