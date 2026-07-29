---
layout: post
title: "Routing content generation with LLMs"
tags: [llm, architecture, microservices, content]
---

Hey everyone,

I wanted to share a small technical detail from behind the scenes of my content sites. When I started building out the generation pipeline, the goal was to avoid a monolithic LLM dependency, especially as new models emerge and specialized ones become more prominent.

The core of it is a simple LLM router. Instead of sending every generation request to the same model, the router takes the article type as input. Based on that, it directs the request to a specific LLM endpoint. For instance, an article destined for [qepam.com](https://qepam.com), like a deep dive into Roth IRAs, might go to a model fine-tuned for clarity and factual accuracy in financial explanations. On the other hand, the more creative, editorial summaries you see on [aceju.com](https://aceju.com) for new AI tools might be handled by a different model, perhaps one better at concise, engaging prose.

This isn't about using the 'best' model everywhere, but the 'right' one for the specific task. The interesting part is the fallback cascade. If the primary model for a given article type is unavailable, or if an API call fails, the router automatically cycles through a predefined list of alternatives. It's a simple retry mechanism that ensures generation doesn't stall, even if one specific API goes down temporarily. I've found this adds a surprising amount of resilience to the overall system without much overhead.

Happy to answer any questions about this routing approach.