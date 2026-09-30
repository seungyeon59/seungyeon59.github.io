---
layout: page
title: "JoyWalk: Walking Routes for Small Happiness"
description: "Best Use of API (Vultr) · HackCMU 2026 · Team OdyssAI"
img: assets/img/joywalk_architecture.jpg
importance: 3
category: research
related_publications: false
---

Navigation apps optimize for speed, so they skip the small, unexpected joys along the way. JoyWalk is a walking-route app built around the Korean idea of *so-hwak-haeng*, "small but certain happiness." Instead of the fastest path, it routes you past nearby **Joy Spots**: a friendly dog someone photographed, cherry blossoms in bloom, a cozy café, small moments other people have left behind. Built in 24 hours at **HackCMU 2026** (Sept 11&ndash;12), it won **Best Use of API (Vultr)**.

<div>
  <a href="https://joywalk-small-happiness.dyheo619.chatgpt.site/" class="btn btn-sm z-depth-0" role="button">Live Demo</a>
  <a href="https://youtu.be/2Iy9umJSEdc" class="btn btn-sm z-depth-0" role="button">Video</a>
  <a href="https://github.com/seungyeon59/Small-Happiness/blob/main/docs/HackCMU-Slides.pdf" class="btn btn-sm z-depth-0" role="button">Slides</a>
  <a href="https://github.com/seungyeon59/Small-Happiness" class="btn btn-sm z-depth-0" role="button">Code</a>
</div>

## The Joy Map

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/joywalk.jpg" class="img-fluid rounded z-depth-1" zoomable=true alt="JoyWalk's main map of Pittsburgh with glowing joy bubbles, category filters, a search bar and a camera button." %}
  </div>
</div>
<div class="caption">
  Small joys shared by other people appear as glowing bubbles on the map, filterable by category.
</div>

Anyone can leave a joy right where they stand: take a photo or pick one from the album, write a line, and the app suggests a matching emoji from the keywords ("the coffee smell here is amazing" becomes ☕). The pin appears on the map immediately and can be recommended into other people's routes. The interface uses spring animations and glassmorphism inspired by Apple's Fluid Interface language, with a dark "dopamine palette" of purple, pink and lime.

## Joy routes

<div class="row justify-content-sm-center">
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/joywalk_routes.jpg" class="img-fluid rounded z-depth-1" zoomable=true alt="Route recommendation panel showing a map with a detour route and three route styles: flavor-first, distance-first and balanced." %}
  </div>
</div>
<div class="caption">
  Given a start and a destination, JoyWalk proposes several route styles: flavor-first, distance-first, or balanced.
</div>

Nearby Joy Spots are first personalized with **hybrid collaborative filtering**. The visiting order is then optimized as a small **Hamiltonian-path problem**, and walking directions, distance and duration come from the Google Maps Directions API.

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/joywalk_routing.jpg" class="img-fluid rounded z-depth-1" zoomable=true alt="Four-step routing pipeline: a padded corridor around the direct route, a distance matrix, a brute-force search over the order of joy bubbles, and the optimized result." %}
  </div>
</div>
<div class="caption">
  Joy spots near the direct route are gathered into a corridor and turned into a distance matrix. The start and end stay fixed, and only the order of the joy spots is optimized.
</div>

## Real-time discovery with Grok

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/joywalk_spot.jpg" class="img-fluid rounded z-depth-1" zoomable=true alt="A joy spot detail card for a skyline view at PNC Park, tagged as discovered by Grok on X." %}
  </div>
</div>
<div class="caption">
  A spot discovered automatically from a public X post, with its story, photo and tags.
</div>

On the server, xAI's Grok (`grok-4.6`) with the `x_search` tool scans recent public X posts from Pittsburgh. Only results with a publicly visitable location and a verifiable post link become map bubbles. Results are cached for 6 hours and community spots are always shown first, so API latency or rate limits never break the demo, and the API key stays server-side.

## System

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/joywalk_architecture.jpg" class="img-fluid rounded z-depth-1" zoomable=true alt="Architecture diagram: a Next.js client and API layer connected to Firebase, MongoDB, Google Maps, X/Grok, Gemini and Google Translate." %}
  </div>
</div>
<div class="caption">
  The Next.js API layer sits between the client and every external service: Firebase for auth and photos, MongoDB for joy data, Google Maps for routing, and Grok, Gemini and Translate for discovery and enrichment.
</div>

Recommendation differences are currently demonstrated with 15 mock users and 3 demo personas. The next step is to replace them with real like and visit events streamed into Firestore.

**Tech:** Next.js, React, TailwindCSS, Google Maps Platform, xAI Grok, Firebase, MongoDB

**Team OdyssAI:** Doyoung Heo, Yucheon Park, Minki Kim, Seungyeon Back
