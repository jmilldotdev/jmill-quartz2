---
aliases:
  - Haven Studios generative escape rooms
tags:
  - sources/bookmark
URL: https://sonyinteractive.com/en/news/blog/haven-studios-experimenting-with-ml-driven-escape-room-games/
related:
  - "[[🗺️ LLM Games|LLM Games]]"
publish: true
created: 2025-06-27 07:26
---

AI-driven text games are as old as language models that can string sentences together. You can just ask a chat model to lead you through a story. The addition of text-to-image models allowed these scenarios to be illustrated. What these experiences lack, however, is the ability to interact with the imagery and hard checks on your actions. They are fundamentally a textual conversation where, more or less, anything goes.

What would it take to replicate the old point-and-click adventure games (or a hidden object game)? Are the model capabilities there yet? To explore this, we created a browser game prototype that creates a scene with objects in response to prompts from the player and makes a short escape room puzzle out of it. The items are clickable and the scene responds to item interactions.

In this post, we’ll give an overview of the experience then dive into how we combined ML models and strategies to realize it.