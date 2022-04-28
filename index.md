---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
--- 

This is the homepage for the new [Reproducibility Track](https://2022.naacl.org/blog/reproducibility-track/) introduced at [NAACL 2022](https://2022.naacl.org/). If you are interested in participating, please join our [Slack workspace](https://join.slack.com/t/cs-b5i1449/shared_invite/zt-16nrrhflc-gPPQwvU7OQCEoO8YG393Ng). You can also reach us [via email](mailto:naacl-2022-reproducibility-track@googlegroups.com). Please submit the relevant information required to participate in [this form](https://forms.office.com/pages/responsepage.aspx?id=DQSIkWdsW0yxEjajBLZtrQAAAAAAAAAAAAO__QPVZQtUMlgwWktNSVo0NVBDQ1JXTkdESFc4NFdBWC4u).

<!-- Output copied to clipboard! -->

<!-----
NEW: Check the "Suppress top comment" option to remove this info from the output.

Conversion time: 0.639 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β31
* Thu Dec 16 2021 06:57:03 GMT-0800 (PST)
* Source doc: Reproducibility Track NAACL 2022
----->

## Important Dates

| Deadline |  | 
| ----------- | ----------- |
| April 7     | Submission window begins. The form to submit to the track can be found [here](https://forms.office.com/pages/responsepage.aspx?id=DQSIkWdsW0yxEjajBLZtrQAAAAAAAAAAAAO__QPVZQtUMlgwWktNSVo0NVBDQ1JXTkdESFc4NFdBWC4u). |
| April 12   | Sign up for the Reproducible Results Badge [here](https://forms.office.com/r/i88YsKM58i). This form is to gauge interest in participation. You may still apply for the Reproducible Results Badge if you do not sign up by this date. |
| April 19 | Office hours to help with submissions announced. Please see [here](/pages/office-hours.html) for times |
| May 10 | Submissions for **main conference papers** (including Findings) are due (updated from May 3). You may submit to the track [here](https://forms.office.com/pages/responsepage.aspx?id=DQSIkWdsW0yxEjajBLZtrQAAAAAAAAAAAAO__QPVZQtUMlgwWktNSVo0NVBDQ1JXTkdESFc4NFdBWC4u) |
| May 18 | Submission deadline for **demo papers**. You may submit to the track [here](https://forms.office.com/pages/responsepage.aspx?id=DQSIkWdsW0yxEjajBLZtrQAAAAAAAAAAAAO__QPVZQtUMlgwWktNSVo0NVBDQ1JXTkdESFc4NFdBWC4u) |
| May 20 | Badge notification date for main conference papers |
| May 28 | Badge notification date for demo papers |

**TLDR;** After notification of acceptance and before the camera ready is due authors will have the option to earn up to three reproducibility “badges” by 1) providing a link to code, 2) providing a link to a trained model, and 3) participating in a verification process where a trained model will replicate some result from the paper. 

## Track

This track introduces a badge system to formalize expectations around reproducibility of our commmunity’s research findings. The main idea is to incentivize authors of [NAACL 2022](https://2022.naacl.org/) papers to release models, code, and other information necessary to reproduce the main results/findings of their papers. We outline the details of the track here.

### What are these reproducibility badges?

The papers accepted to the NAACL main conference and Findings can apply for three types of badges.

**1) Open-Source Code Badge**: Authors submit a link to code. The code itself will not be run by reviewers (though it may be visually checked), so it is up to the authors to provide appropriate documentation. We recommend authors check the PapersWithCode code completeness checklist [here](https://medium.com/paperswithcode/ml-code-completeness-checklist-e9127b168501).

**2) Trained Model Badge**: Authors submit a link to download a trained model. Similar to the Open-Source Code Badge, the model will not be run by reviewers, though other aspects (e.g. size on disk) will be checked to confirm that the provided link works.

**3) Reproducible Results Badge**: Authors verify that their model replicates a result they specify from their paper. Authors will package a trained model into a Docker container and submit the container to a server where it will be executed automatically. The server will execute the container and verify that its output matches a result from the author’s paper. In addition to detailed guidelines and materials, the track will also provide compute resources, a discussion forum, and office hours to facilitate this. A tutorial for how to participate in this process and apply for the Reproducible Results badge can be found [here](/tutorial). Information about office hours for helping you apply for this badge can be found [here](/pages/office-hours.html).

The primary goals of these three badges are to formalize how authors release code and trained models, and to make it easier for other researchers to find and use them. These badges build on the suggested [badges](https://www.acm.org/publications/policies/artifact-review-badging) from the ACM. The first two badges are types of “Artifact Available” badges which indicate that authors make some (unverified) materials available, and the third is a “Results Replicated” badge also meant to provide a working runtime environment so future researchers can easily build on or compare against the published work.

### Why do we need this track?

Our progress as a scientific discipline rests on the reproducibility of our scientific claims. Sharing code and trained models facilitates comparisons against previous work, and gives starting implementations for new research to build on. Furthermore, with the rapid rise in computational cost of our experiments, releasing trained models saves costs of rerunning experiments others have already run. This track is aimed at (a) incentivizing authors to facilitate reproducibility, and (b) introducing some formalization of the process and our expectations for reproducible research as a community.

### What is the benefit to authors?

The main benefit to authors is in making their work reproducible in a way that will enable broader adoption of their work. In addition, NAACL will highlight the papers that successfully participated in the track via highlighting badged papers in a special section of the website, through promotion online and during the conference, and other similar avenues.

### FAQ

**Q**: Does this disadvantage papers that can’t achieve these badges? 

**A**: No. These badges should only be considered for a subset of all papers presented at NAACL; there are many types of papers for which it’s not appropriate to submit, for example, an executable model. Papers which introduce a dataset, papers which primarily focus on linguistic or mathematical theory, papers from industry labs that can’t publicly release scientific artifacts, and position papers are all types of papers that we value as a community that likely won’t be covered by these badges.

**Q**: Do I need to earn Badge 1 to get Badge 2, or Badge 2 to get Badge 3? 

**A**: No, authors can earn any subset of the three badges.

**Q**: What if I can’t publicly release my model or data, but still want to earn Badge 3 (showing my results are reproducible)? 

**A**: That’s great. Everything submitted for Badge 3 will be deleted after verification, and will not be made public.

**Q**: Do I need to anonymize the code, model, or executable?

**A**: No. This process will take place after notification of acceptance, so it will not interact with double-blind reviewing of the paper. In addition, much of this process will be automatic, and badge reviewers will only check to confirm that, for example, the links authors provide work as intended, and that there aren’t errors in the automatic verification process.

**Q**: Are papers accepted to Findings able to participate?

**A**: Yes.
