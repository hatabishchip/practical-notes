---
layout: post
title: "GSC-driven topic selection"
tags: [seo, content, gsc, network]
---

These days I let Google Search Console do most of the heavy lifting when I decide what to write for the network. I pull the performance report for each property, filter for queries that have impressions but low CTR, and then look at the average position. If a query sits around position 5‑10 and has a decent impression count, I treat it as a low‑effort win: the audience is already searching for that phrase, I just need to provide a better match.

The workflow is simple. I export the CSV from GSC, run a small script that groups queries by page and sorts by impression count. I set a threshold of 500 impressions per month and a position above 8 to surface topics that are popular but not saturated. The script then outputs a markdown list that I paste into my editorial backlog. Because the list is derived from actual search data, I rarely have to guess what people want.

I use this method across the whole network, from the pet‑care guides at [practical pet care guides](https://fumpe.com) to the coffee brewing tutorials at [coffee brewing and gear guides](https://dreqo.com). It keeps the content pipeline lean and the SEO results predictable.

If you’re curious about the exact script or the thresholds I use, just let me know.