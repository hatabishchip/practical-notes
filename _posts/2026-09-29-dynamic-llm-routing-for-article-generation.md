---
layout: post
title: "Dynamic LLM routing for article generation"
tags: [llm, router, content, tech]
---

Recently I added a small router in the generation pipeline of my content-site network. The router looks at the article type - finance guide, editorial award, tutorial - and selects a model that is tuned for that style. For finance guides (e.g., [qepam.com](https://qepam.com)) I use a 7B instruction model that has been fine-tuned on plain-English explanations. For editorial awards (see [aceju.com](https://aceju.com)) I switch to a larger 13B model that handles nuanced opinion and ranking language better.

The router is just a few lines of Python that maps a string label to a model ID, then calls the appropriate endpoint. The trick that keeps the system from hanging is the fallback cascade. If the primary model returns an error, times out, or produces an empty completion, the router automatically retries with a more generic model (a 3B base) before giving up. I also added a short exponential back-off so repeated failures don't flood the API.

Because the fallback is built into the same request loop, the rest of the pipeline - markdown conversion, image insertion, SEO tags - never sees a missing body. In practice I've seen the latency increase by only a few hundred milliseconds when a fallback fires.

I log each fallback event so I can see patterns over time and adjust model assignments as needed.

If you're curious about the routing logic or the error-handling code, feel free to ask.