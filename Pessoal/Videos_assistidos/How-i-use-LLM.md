---
tags:
---
How to see the ranking of LLM:
https://arena.ai/
https://labs.scale.com/leaderboard

Text inputs are broken down into tokens - https://tiktokenizer.vercel.app/
and then the model answer with tokens.

This group of user tokens and assistant tokens will generate a token stream - **context window**.

**pre-training**: 3 months of training on internet documents.
**post-training**: SFT, RLHF, RL on Conversations.

O LLM apenas é um grande arquivo que quando executado prevê qual será o próximo token que deve ser respondido. Desse modo, podemos pensar nele como um modelo que lembra vagamente de informações que estão na internet.

Sempre que você tiver mudando de contexto, o ideal seria iniciar um novo chat.