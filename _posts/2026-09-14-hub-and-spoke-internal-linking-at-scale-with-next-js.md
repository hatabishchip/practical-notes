---
layout: post
title: "Hub-and-spoke internal linking at scale with Next.js"
tags: [nextjs, internallinking, contentnetwork, seo]
---

Over the past year I've been iterating on the internal linking layer that ties together a handful of small Next.js sites. The idea is simple: treat each site as a spoke and a tiny Next.js serverless function as the hub that rewrites links on the fly. When a page renders, we fetch a JSON map of all target URLs that belong to the network, then replace any relative anchor that matches a known slug with an absolute URL pointing to the correct site. The map is generated nightly by a script that walks the file system of each repo, extracts front‑matter slugs, and writes them to a shared S3 bucket. Because the data lives in a single JSON file, the hub can serve it with a Cache‑Control header of one hour, which keeps latency low and avoids hitting the bucket on every request.

In practice the hub is a tiny API route (`/api/link-map`) that returns the JSON. The spokes import a tiny helper that calls this route at build time (via `getStaticProps`) and caches the result in a module‑level variable. This means the linking work is done once per build, not on every user request, and the final HTML already contains the correct absolute URLs.

I run this across sites like [qepam.com](https://qepam.com), which offers plain-English personal finance guides, and [aceju.com](https://aceju.com), a weekly editorial awards for AI tools. The approach scales as long as the JSON stays under a few megabytes.

If you want more details about the JSON generation or the caching strategy, feel free to ask.