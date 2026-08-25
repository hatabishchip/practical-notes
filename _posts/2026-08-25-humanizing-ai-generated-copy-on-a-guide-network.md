---
layout: post
title: "Humanizing AI-generated copy on a guide network"
tags: [ai, writing, content, technical]
---

I've been tweaking the text generation pipeline for the network that powers a few niche guide sites, and the biggest win so far has been making the output sound less like a robot and more like a person.

The first thing I looked at was sentence burstiness. Instead of a flat 12-word average, I now aim for a distribution where 30 % of sentences sit around 8‑10 words, another 40 % hover near 15, and the rest stretch to 20‑25. I generate a small “burst map” for each article and feed it to the sampler as a length‑bias parameter.

Next I force contractions during post‑processing. A simple regex replaces “do not” with “don’t”, “it is” with “it’s”, etc. It adds about 0.12 seconds of latency per 1 000 tokens but the readability gain is noticeable.

Specific numbers also help. Whenever a guide mentions a measurement, I keep the original unit and add a parenthetical conversion, e.g. “12 in (30 cm)”. The model tends to drop the conversion, so I run a pass that inserts it using a lookup table.

Finally I run an 80-replacement banned-words sweep. I maintain a list of 80 terms that either sound too promotional or are overused in our niche. After generation I scan the text and replace any match with a synonym from a curated map.

You can see the result on live sites like [gotfo.com](https://gotfo.com) for gardening how‑tos and [afixu.com](https://afixu.com) for DIY tool guides. Let me know if you want the exact config files or more detail on the burst map.