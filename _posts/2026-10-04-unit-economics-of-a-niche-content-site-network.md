---
layout: post
title: "Unit economics of a niche content-site network"
tags: [content, economics, tech, startup]
---

I run a small network of niche how-to sites. Right now the two live examples are [fumpe.com](https://fumpe.com), a practical pet-care guide, and [dreqo.com](https://dreqo.com), a coffee-brewing and gear guide. Both sit on the same stack: a static site generator, Cloudflare CDN and a tiny MySQL instance for comments.

At the moment each site gets about 12 k unique visitors per month, with an average CPM of $4.5 from a mix of AdSense and direct sponsorships. That translates to roughly $540 in ad revenue per site per month. The biggest cost is content creation: I pay $0.08 per word to freelance writers and aim for 3 000 words per month per site, which is $240. Hosting and domain fees are about $30 per month for the pair, and the MySQL instance adds $15. In total the monthly burn is $285 per site, leaving a $255 margin.

The financial model to reach $30 k/mo run-rate by month 24 assumes we scale to 20 similar sites, each hitting 15 k visitors and a modest CPM increase to $5 as the audience matures. At that point gross revenue would be 20 × 15 000 ÷ 1 000 × $5 = $1 500 per month per site, or $30 k total, while the incremental cost per new site stays around $300 because the infrastructure is shared.

I keep a simple spreadsheet to track CAC, LTV and break-even month for each property. If you want to see the numbers or discuss the stack, let me know.