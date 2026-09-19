---
layout: post
title: "Nightly prompt rewrite using Search Console"
tags: [automation, seo, python, content]
---

I’ve been tinkering with a small agent that updates the prompts we use to generate new articles for our network of content sites. Every night it pulls the latest performance data from Google Search Console, looks for queries that are rising or dropping, and rewrites the seed prompts accordingly. The idea is to keep the topics aligned with what users are actually searching for, without having to manually edit dozens of prompt files.

The pipeline is a few Python scripts. First a cron job runs `search_console_report.py` which authenticates with the Search Console API and downloads the last 30 days of clicks, impressions and average position for each query. The script then filters for queries with a click-through-rate above 2% and a position improvement of at least three spots. Those queries are fed into a tiny LLM prompt that says "turn this search query into a content brief for a how-to article". The LLM returns a revised prompt, which we store in a JSON file keyed by the target URL.

Each site reads its own JSON file at build time. For example, the home-gardening how-tos on [gotfo.com](https://gotfo.com) and the DIY tool guides on [afixu.com](https://afixu.com) both pull the latest prompt before the static generator runs. Because the JSON is regenerated nightly, the next build automatically reflects the newest search trends.

I keep the agent deliberately simple - a few hundred lines, no orchestration framework - so it’s easy to tweak. Feel free to ask if you want more details about the data processing or the prompt-generation step.