---
layout: post
title: "Nightly prompt rewrite from Search Console data"
tags: [content, automation, search, analytics]
---

I've been running a small network of content sites for the last two years. The part that has taken the most time is keeping the editorial prompts in sync with what people actually search for. To automate that, I built a tiny agent that runs every night.

The agent pulls the latest Click-through-Rate and impression data from Google Search Console for each property. It filters out queries that have at least 50 impressions and a CTR below 2 %. Those signals usually indicate a missed opportunity. For each such query the script generates a new prompt: a short title, a target keyword list and a brief outline. The prompt is written to a JSON file that the content pipeline reads the next morning.

I keep the logic in a single Python module (about 120 lines). The nightly job is scheduled with cron on a cheap VPS. The module uses the official Search Console API, pandas for aggregation and Jinja2 to render the prompt template. After the file is written I push it to a git branch that the static site generator watches, so the next build includes the updated prompt.

The system has been running on two of my sites - practical pet care guides at [fumpe.com](https://fumpe.com) and coffee brewing guides at [dreqo.com](https://dreqo.com) - without manual intervention for three months.

If you want more details about the API calls or the template logic, let me know.