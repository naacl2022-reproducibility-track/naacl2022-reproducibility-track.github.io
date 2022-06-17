---
layout: page
title: Badges
permalink: /badges/
order: 2
header: true
---

### What are these reproducibility badges?

The papers accepted to the NAACL conference can apply for three types of badges.

### Open Source Code Badge
<div style="display: flex; align-items:center">
  <img style="vertical-align: middle; margin-right: 10pt;" src="/assets/images/code-badge.png" height="100" width="100">
  <span style="">Authors submit a link to code. The code itself will not be run by reviewers (though it may be visually checked), so it is up to the authors to provide appropriate documentation. We recommend authors check the PapersWithCode code completeness checklist <a href="https://medium.com/paperswithcode/ml-code-completeness-checklist-e9127b168501">here</a>.</span>
</div>
<br>

### Trained Model Badge
<div style="display: flex; align-items:center">
  <img style="vertical-align: middle; margin-right: 10pt;" src="/assets/images/model-badge.png" height="100" width="100">
  <span style="">Authors submit a link to download a trained model. Similar to the Open-Source Code Badge, the model will not be run by reviewers, though other aspects (e.g. size on disk) will be checked to confirm that the provided link works.</span>
</div>
<br>

### Reproducible Results Badge
<div style="display: flex; align-items:center">
  <img style="margin-right: 10pt;" src="/assets/images/repro-results-badge.png" height="100" width="160">
  <span style="">Authors verify that their model replicates a result they specify from their paper. Authors will package a trained model into a Docker container and submit the container to a server where it will be executed automatically. The server will execute the container and verify that its output matches a result from the author’s paper. In addition to detailed guidelines and materials, the track will also provide compute resources, a discussion forum, and office hours to facilitate this. A tutorial for how to participate in this process and apply for the Reproducible Results badge can be found [here](/tutorial). Information about office hours for helping you apply for this badge can be found <a href="/pages/office-hours.html">here</a>.</span>
</div>
<br>

### Goals
The primary goals of these three badges are to formalize how authors release code and trained models, and to make it easier for other researchers to find and use them. These badges build on the suggested [badges](https://www.acm.org/publications/policies/artifact-review-badging) from the ACM. The first two badges are types of “Artifact Available” badges which indicate that authors make some (unverified) materials available, and the third is a “Results Replicated” badge also meant to provide a working runtime environment so future researchers can easily build on or compare against the published work.