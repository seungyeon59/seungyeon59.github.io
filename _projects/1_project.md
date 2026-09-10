---
layout: page
title: GraphRAG-based Real-Time Recommendation
description: Graduate Researcher · in collaboration with LG Electronics · Jan 2026 – Present
img: assets/img/graphrag.png
importance: 1
category: research
related_publications: false
---

As a **Graduate Researcher** on a _GraphRAG-based Recommendation System_ (in collaboration with **LG Electronics**, Jan 2026 – Present), I am building a graph-based retrieval and reasoning pipeline for real-time recommendation of news and OTT content.

<div class="row justify-content-sm-center">
  <div class="col-sm-12 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/graphrag.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Pipeline from trending-search news detection through a news-content graph to an LLM that explains each recommendation." %}
  </div>
</div>
<div class="caption">
  Trending news are scored by a trend detector, linked into a news&ndash;content graph over shared topics and people, and the retrieved candidates are passed to an LLM that reasons over the graph path to explain the recommendation.
</div>

**Key contributions**

- Built a **real-time data pipeline** for news and OTT content ingestion and processing.
- Designed a **dual-graph framework** aligning news–content graphs via shared entities.
- Developed a **graph-based retrieval pipeline** using multi-hop traversal to generate candidate content.
- Integrated **LLMs for path-based reasoning** over graph structures, enabling explainable recommendations.
