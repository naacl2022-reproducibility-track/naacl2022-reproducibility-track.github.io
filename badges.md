---
layout: page
title: Badges
permalink: /badges/
order: 2
header: true
---

### What are these reproducibility badges?

The papers accepted to the NAACL conference can apply for three types of badges.

**1) Open-Source Code Badge**: Authors submit a link to code. The code itself will not be run by reviewers (though it may be visually checked), so it is up to the authors to provide appropriate documentation. We recommend authors check the PapersWithCode code completeness checklist [here](https://medium.com/paperswithcode/ml-code-completeness-checklist-e9127b168501).

**2) Trained Model Badge**: Authors submit a link to download a trained model. Similar to the Open-Source Code Badge, the model will not be run by reviewers, though other aspects (e.g. size on disk) will be checked to confirm that the provided link works.

**3) Reproducible Results Badge**: Authors verify that their model replicates a result they specify from their paper. Authors will package a trained model into a Docker container and submit the container to a server where it will be executed automatically. The server will execute the container and verify that its output matches a result from the author’s paper. In addition to detailed guidelines and materials, the track will also provide compute resources, a discussion forum, and office hours to facilitate this. A tutorial for how to participate in this process and apply for the Reproducible Results badge can be found [here](/tutorial).

The primary goals of these three badges are to formalize how authors release code and trained models, and to make it easier for other researchers to find and use them. These badges build on the suggested [badges](https://www.acm.org/publications/policies/artifact-review-badging) from the ACM. The first two badges are types of “Artifact Available” badges which indicate that authors make some (unverified) materials available, and the third is a “Results Replicated” badge also meant to provide a working runtime environment so future researchers can easily build on or compare against the published work.