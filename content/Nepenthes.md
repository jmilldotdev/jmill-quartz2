---
aliases:
  - Nepenthes
tags:
  - sources/bookmark
URL: https://zadzmo.org/code/nepenthes/
related:
  - "[[current AI defending itself or confusing future, smarter ai]]"
publish: true
created: 2025-05-02 11:15
---

This is a tarpit intended to catch web crawlers. Specifically, it's targetting crawlers that scrape data for LLMs - but really, like the plants it is named after, it'll eat just about anything that finds it's way inside.

It works by generating an endless sequences of pages, each of which with dozens of links, that simply go back into a the tarpit. Pages are randomly generated, but in a deterministic way, causing them to appear to be flat files that never change. Intentional delay is added to prevent crawlers from bogging down your server, in addition to wasting their time. Lastly, optional Markov-babble can be added to the pages, to give the crawlers something to scrape up and train their LLMs on, hopefully accelerating model collapse.