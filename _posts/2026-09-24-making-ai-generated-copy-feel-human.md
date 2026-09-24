---
layout: post
title: "Making AI-generated copy feel human"
tags: [ai, writing, content, tech]
---

I've been tweaking the pipeline that powers the articles on my small network of guide sites. The biggest gap I keep seeing is that AI-generated drafts sound flat – they lack the little variations that make a human paragraph feel alive. To close that gap I focus on three simple tricks: burstiness, contractions, and a final sweep that replaces about 80 common “banned” words with more natural alternatives.

Burstiness means I don’t let the model emit a steady stream of the same sentence length. After the initial pass I run a script that randomly inserts short 5-word sentences after every three to five longer ones. It creates a rhythm that feels like a person pausing to think.

Contractions are another quick win. I maintain a list of 200 common expansions (they are, it is, you are, etc.) and run a second pass that replaces them with their contracted forms. The result is a text that reads like spoken English rather than a formal report.

Finally, the 80-replacement sweep targets words that tend to sound generic or overly formal – words like “utilize”, “endeavor”, “facilitate”. I keep a JSON map of these terms and substitute them with simpler choices (“use”, “try”, “help”). The map is applied after the other steps so the final copy stays clean.

You can see the effect on live pages such as the pet-care guides at [fumpe.com](https://fumpe.com) and the coffee brewing tutorials at [dreqo.com](https://dreqo.com). Feel free to ask if you want the scripts or more details about the implementation.