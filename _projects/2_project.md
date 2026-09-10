---
layout: page
title: "AdapDict: Level- and Domain-Adaptive Educational Dictionary"
description: "Co-first author · CSCW 2026 (Accepted)"
img: assets/img/adapdict.jpeg
importance: 2
category: research
related_publications: true
---

A user-adaptive and reliable LLM-based system for personalized dictionaries and encyclopedia entries.

<div>
  <a href="https://adapdict-87k5.onrender.com" class="btn btn-sm z-depth-0" role="button">Web Demo</a>
  <a href="https://github.com/maenwi/AdapDict" class="btn btn-sm z-depth-0" role="button">Code</a>
</div>
<div class="caption" style="text-align: left; margin-top: 0.25rem;">
  The demo is hosted on a free Render instance that sleeps when idle, so the first request can take up to a minute to wake it.
</div>

<div class="row justify-content-sm-center">
  <div class="col-sm-12 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/adapdict.jpeg" class="img-fluid rounded z-depth-1" zoomable=true alt="A query is analyzed for native and target language, adapted to the user's field and level, then generated and checked by a verifier before the explanation is returned." %}
  </div>
</div>
<div class="caption">
  The query analyzer infers the native and target language, the user prompt adaptor conditions on the reader's field and level, and a generator&ndash;verifier loop returns an error message and regenerates whenever the draft fails validation.
</div>

- Proposed a level- and domain-adaptive explanation framework for controllable explanation generation in LLMs.
- Designed a generator–verifier loop with structured outputs, reducing hallucination by 50%.
- Developed a user-adaptive prompting mechanism for multi-dimensional control of explanation difficulty.
- Conducted a user study (n=41) demonstrating improved clarity, usability, and domain-specific understanding over baseline tools.

{% cite adapdict2026 %}
