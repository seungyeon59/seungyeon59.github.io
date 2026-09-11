---
layout: page
title: "AdapDict: Level- and Domain-Adaptive Educational Dictionary"
description: "Co-first author · CSCW 2026 (Accepted)"
img: assets/img/adapdict.jpeg
importance: 2
category: research
related_publications: true
---

In a study group or a classroom, people of very different backgrounds read the same material. Dictionaries, machine translation and encyclopedias answer all of them identically, and LLM chat tools answer well only for those who can write a good prompt — so the gap between a novice and an expert in the same room stays open. AdapDict lets a learner state their level and domain instead of engineering a prompt, and returns a structured explanation built for that reader.

<div>
  <a href="https://adapdict-87k5.onrender.com" class="btn btn-sm z-depth-0" role="button">Web Demo</a>
  <a href="https://github.com/maenwi/AdapDict" class="btn btn-sm z-depth-0" role="button">Code</a>
</div>
<div class="caption" style="text-align: left; margin-top: 0.25rem;">
  The demo is hosted on a free Render instance that sleeps when idle, so the first request can take up to a minute to wake it.
</div>

## How it works

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/adapdict.jpeg" class="img-fluid rounded z-depth-1" zoomable=true alt="A query is analyzed for type and language, adapted to the user's level and domain, validated, then generated and checked by a verifier before the explanation is returned." %}
  </div>
</div>
<div class="caption">
  The pipeline's four components: Query Analyzer, User Prompt Adaptor, Query Validation, and the Generator&ndash;Verifier loop.
</div>

The **Query Analyzer** decides whether the input is a word, a sentence or a paragraph and detects its language; that classification determines the shape of the output. The **User Prompt Adaptor** then builds the prompt from a three-part profile — one of six learning levels (elementary through doctoral), an optional domain, and the language direction. Levels are not a single knob: each is mapped onto five aspects of explanatory complexity — vocabulary, sentence structure, explanation structure, abstraction level, and use of examples — grounded in educational and cognitive science.

Reliability is handled in two stages. **Query Validation** sorts every query into valid, typo, factual error, ambiguous or nonsense, returning correction or clarification rather than letting the generator answer a broken question. The **Generator** (Gemini-2.5-Flash) then emits JSON that follows a fixed schema, and a **Hallucination Verifier** scores that first draft for hallucination severity from 0 to 1, triggering one regeneration above a threshold of 0.4. Evaluated on 180 queries, the verifier cut hallucinated dictionary outputs from 40% to 20% — a 50% relative reduction — with detection accuracy between 0.92 and 0.98 across middle, bachelor and doctoral levels. Encyclopedia queries showed no first-stage hallucinations at all, likely because they draw on common knowledge already encoded in pre-training.

AdapDict runs in Korean, English, Chinese and German, in two modes: Dictionary, which translates and explains with usage examples in either direction, and Encyclopedia, which gives conceptual explanations and background in the reader's own language.

## The interface

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/adapdict_ui.png" class="img-fluid rounded z-depth-1" zoomable=true alt="The AdapDict web interface: language, level and field selectors above a query box, a search summary, and a results panel of sentence and word cards." %}
  </div>
</div>
<div class="caption">
  Input screen: mode toggle, language pair (a), level and domain (b), query (c). Results screen: a card-based panel, with sharing options (d).
</div>

The results screen never returns one block of prose. A word query produces a **word card** — translation, domain-specific meaning, alternative expressions, example sentences. A sentence produces a **sentence card** with the full translation and explanation, followed by word cards for the key vocabulary in it. A paragraph nests all three: a paragraph card, then sentence-by-sentence breakdowns, then the word cards. A learner can read the whole thing, drop to the sentence that lost them, then to the single term inside it — each level written at the difficulty they asked for.

The sharing options in (d) are a deliberate design choice rather than a convenience. Since coordinating knowledge exchange in a group depends on being aware of what the others know, URL copy and Save as PDF let group members hand each other explanations of the same passage at their own levels.

## User study

<div class="row justify-content-sm-center">
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/adapdict_userstudy.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Bar charts comparing AdapDict against baseline tools across four tasks, plus Likert ratings of AdapDict's own features." %}
  </div>
</div>
<div class="caption">
  Preference scores against the baselines (top) and Likert ratings of AdapDict's own features (bottom).
</div>

41 participants — undergraduates, master's and PhD students, job seekers and employees — completed four tasks spanning both modes at word and paragraph level. Each task was compared against the baselines that actually fit it: Google Translate and the Cambridge Dictionary for dictionary word lookup, Google Translate and DeepL for paragraphs, Wikipedia for encyclopedia terms, and ChatGPT for encyclopedia paragraphs. Responses were converted into a preference score that is positive when AdapDict was preferred and negative when a baseline was.

Ratings held up across occupational groups: mean Likert scores exceeded 4.0 in nearly every cell, and a Kruskal–Wallis test found no significant difference between groups. 85% of participants rated AdapDict more learning-friendly than existing tools, and 85% intended to keep using it. Level control was genuinely exercised rather than left at a default — over 95% used at least two levels and 68% used three or more — and it won 97.6% of dictionary word-level comparisons and 87.8% at paragraph level, with domain adaptation winning 95.1% of dictionary word-level tasks. In open responses, 22 of 41 named level control and 11 named domain adaptation as the main advantage.

The honest weak spot is encyclopedia paragraphs, where the win rate falls to 56.1%: ChatGPT's longer, more detailed answers were often preferred for comprehension. The win rates should also be read for what they are — most baselines expose no level or domain control at all, so they show that participants valued built-in adaptation, not that AdapDict beats a carefully prompt-engineered ChatGPT, which the study did not test.

## Key contributions

- Proposed a level- and domain-adaptive explanation framework for controllable explanation generation in LLMs.
- Designed a generator–verifier loop with structured outputs, cutting hallucinated dictionary outputs from 40% to 20%.
- Developed a user-adaptive prompting mechanism for multi-dimensional control of explanation difficulty.
- Conducted a user study (n=41) demonstrating improved clarity, usability, and domain-specific understanding over baseline tools.

{% cite adapdict2026 %}
