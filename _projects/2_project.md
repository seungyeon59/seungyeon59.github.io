---
layout: page
title: "AdapDict: Level- and Domain-Adaptive Educational Dictionary"
description: "Co-first author · CSCW 2026 (Accepted)"
img: assets/img/adapdict.jpeg
importance: 2
category: research
related_publications: true
---

A user-adaptive and reliable LLM-based system for personalized dictionaries and encyclopedia entries. A learner tells AdapDict what they already know — their field and their level — and every translation, definition and explanation is generated to match.

<div>
  <a href="https://adapdict-87k5.onrender.com" class="btn btn-sm z-depth-0" role="button">Web Demo</a>
  <a href="https://github.com/maenwi/AdapDict" class="btn btn-sm z-depth-0" role="button">Code</a>
</div>
<div class="caption" style="text-align: left; margin-top: 0.25rem;">
  The demo is hosted on a free Render instance that sleeps when idle, so the first request can take up to a minute to wake it.
</div>

## How it works

<div class="row justify-content-sm-center">
  <div class="col-sm-12 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/adapdict.jpeg" class="img-fluid rounded z-depth-1" zoomable=true alt="A query is analyzed for native and target language, adapted to the user's field and level, then generated and checked by a verifier before the explanation is returned." %}
  </div>
</div>
<div class="caption">
  The query analyzer infers the native and target language, the user prompt adaptor conditions on the reader's field and level, and a generator&ndash;verifier loop returns an error message and regenerates whenever the draft fails validation.
</div>

Two decisions carry the system. The **user prompt adaptor** turns the reader's declared field and level into explicit generation constraints, so "explain photosynthesis" resolves differently for a bachelor's student in biology than for a beginner outside the field. The **generator&ndash;verifier loop** then treats the draft as a proposal rather than an answer: a verifier checks it against the query and the requested level, and an invalid draft is sent back with an error message and guidance instead of being shown. This loop is what reduced hallucination by 50%.

## The interface

<div class="row justify-content-sm-center">
  <div class="col-sm-12 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/adapdict_ui.png" class="img-fluid rounded z-depth-1" zoomable=true alt="The AdapDict web interface: language, level and field selectors above a query box, a search summary, and a results panel of sentence and word cards." %}
  </div>
</div>
<div class="caption">
  Left: a dictionary/encyclopedia toggle, the native and target language pair (a), level and field (b), the query (c), and Copy URL / Save as PDF for keeping a result (d). Right: results are broken into sentence cards, each carrying a translation, an explanation, and word cards with alternative expressions and worked examples.
</div>

Rather than returning one block of prose, AdapDict decomposes a passage into **sentence cards** and, inside them, **word cards**. A learner can read the full translation, then drop to the sentence that lost them, then to the single term inside it — each level explained at the difficulty they asked for. The search summary above the results records which language pair, level and field produced them, so a saved or shared result stays interpretable later.

## User study

<div class="row justify-content-sm-center">
  <div class="col-sm-12 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/adapdict_userstudy.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Bar charts comparing AdapDict against baseline tools across dictionary and encyclopedia tasks, plus Likert ratings of AdapDict's own features." %}
  </div>
</div>
<div class="caption">
  Top four panels: preference for AdapDict over each baseline (&minus;2 to 2, positive favours AdapDict) at word and paragraph level, against Google Translate, the Cambridge Dictionary, DeepL, Wikipedia and ChatGPT. Bottom: ratings of AdapDict's own features on a 1&ndash;5 Likert scale, with the dashed line at the neutral midpoint.
</div>

Across 41 participants, every comparison item came out in AdapDict's favour on average. The margin is clearest on dictionary word-level tasks — domain-appropriate meaning, clarity, and appropriate difficulty all sit near the top of the scale — while the encyclopedia paragraph-level comparison against ChatGPT is the narrowest, with error bars spanning the neutral line on several items. Asked about AdapDict's own features rather than about a competitor, participants rated domain-adaptive explanations and level control the highest.

## Key contributions

- Proposed a level- and domain-adaptive explanation framework for controllable explanation generation in LLMs.
- Designed a generator–verifier loop with structured outputs, reducing hallucination by 50%.
- Developed a user-adaptive prompting mechanism for multi-dimensional control of explanation difficulty.
- Conducted a user study (n=41) demonstrating improved clarity, usability, and domain-specific understanding over baseline tools.

{% cite adapdict2026 %}
