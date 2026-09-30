---
layout: page
title: "Once Upon a Play: An AI Storybook Game for Kids"
description: "SteelHacks XIII 2026 · Workshop paper · Team Steel Hungry"
img: assets/img/onceupon.jpg
importance: 4
category: research
related_publications: false
---

Kids aren't reading as much, and there is a growing worry that AI does their thinking for them. We wanted to flip that: AI doesn't have to replace a child's creativity, it can give that creativity somewhere to go. Once Upon a Play is an interactive story game for children aged 9&ndash;12. They don't just play through a fairy tale, they become the authors who rewrite it, and the AI stages whatever the child imagines. Built in 24 hours at **SteelHacks XIII** (University of Pittsburgh, Sept 19&ndash;20, 2026). The work was later extended into a workshop paper.

<div>
  <a href="https://once-upon-a-play.vercel.app/" class="btn btn-sm z-depth-0" role="button">Live Demo</a>
  <a href="https://youtu.be/aSscBtHs2c8" class="btn btn-sm z-depth-0" role="button">Video</a>
  <a href="https://github.com/seungyeon59/once-upon-a-play/blob/main/docs/assets/SteelHacks_Presentation.pdf" class="btn btn-sm z-depth-0" role="button">Slides</a>
  <a href="https://github.com/seungyeon59/once-upon-a-play" class="btn btn-sm z-depth-0" role="button">Code</a>
</div>

## The game

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/onceupon.jpg" class="img-fluid rounded z-depth-1" zoomable=true alt="The world-select screen of Once Upon a Play with three tale cards: Little Red Riding Hood, Snow White and Cinderella." %}
  </div>
</div>
<div class="caption">
  World select: Little Red Riding Hood, Snow White and Cinderella are playable.
</div>

Kids build stories best when they can *explore a scene*, not just write about it. A blank page asks a child to invent a forest out of nothing, but a forest they are already standing in asks what happens next. So the game is a place to stand in, with the writing happening there.

- **Roles and choices:** Little Red Riding Hood can be played as Red, as Gray the wolf, or as a visitor. Authored choices set story flags that change later scenes and which of three endings you reach.
- **Talk to anyone:** Click a character and type, and Claude answers in that character's voice, knowing the scene, the story so far, and what you already chose.
- **"What happens next?"** Children describe the next scene in their own words, and the story generates a new scene around it, read aloud with ElevenLabs voices.
- **Your drawing, in the story:** Draw a character on paper, photograph it, and it walks into the map. The browser lifts it off the page into a transparent sprite, without an image-generation model.
- **Keep what you made:** At the ending, the whole story is laid out as an illustrated storybook that can be printed or saved as a PDF.

## Letting the model improvise safely

The hard problem was building a map for a story nobody has written yet: the child invents the scene, and the world has to exist a second later. Generating a backdrop image at runtime would arrive in a different style each time and be too slow for a child who is mid-idea. So we inverted it. The world is pre-composed as a closed vocabulary of **36 layered 2.5D backdrops and 54 props** drawn in code, and Claude acts as a casting director rather than a painter. It resolves the child's prompt into an asset assignment: one backdrop, a few props, a position and action for each character, and the resulting story flags.

The server validates every ID, coordinate and flag against that vocabulary before anything renders, so a hallucinated backdrop is rejected rather than drawn. The model improvises the texture, and the authored system owns the state.

Because the players are children, a safety layer screens both directions: the child's input before it reaches Claude, and Claude's output before it reaches the screen. Blocked lines are rolled back out of the story instead of freezing the game.

## System

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/onceupon_architecture.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Architecture diagram: local data and storage, a React and Pixi.js frontend, and an Express backend calling Anthropic Claude, Replicate and ElevenLabs." %}
  </div>
</div>
<div class="caption">
  A React, Zustand and Pixi.js frontend with progress saved in the browser, and an Express API routing requests to Claude and ElevenLabs.
</div>

The team's main takeaway was that the interesting boundary in an AI game is not how much the model can generate, but how narrow you can make its output space and still feel limitless. "Exploration first" engagement and near-zero latency are what keep a child immersed.

**Tech:** React, TypeScript, Zustand, Pixi.js, Express, Anthropic Claude, ElevenLabs, Vercel

**Team Steel Hungry:** Chiyoung Kim, Sumin Shim, Doyoung Heo, Seungyeon Back
