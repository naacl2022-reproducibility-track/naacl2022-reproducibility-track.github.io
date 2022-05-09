---
layout: page
title: Verification Tutorial
permalink: /tutorial/
header: true
order: 1
---

**New:** We are hosting office hours to help you package your code and submit to our verification service.
Please see [this page](/pages/office-hours.html) for office hours times.

The goal of this tutorial is to walk you through how to take the code from your paper, convert it to a reproducible Docker image (which amounts to creating a file that looks like [this](https://github.com/naacl2022-reproducibility-track/reproducibility-example/blob/master/Dockerfile)), and submit the image to the Reproducibility Track's automatic verification tool to earn the Reproducible Results Badge.

**No Docker experience is required to follow this tutorial and earn the badge**;
we expect it should take you about 2 hours to follow if you have never used Docker before.

The tutorial contains the following sections:

1. [Docker Tutorial](/tutorial/docker-tutorial)  
This section explains the basics about Docker and what you need to know about it to participate in the Reproducibility Track.
If you are already familiar with Docker, you can skip this part.

2. [Setting up the Development Environment](/tutorial/development-environment)  
Here we explain how to set up your development environment so that you can build Docker containers, either on the Google Cloud Platform or on your local machine.

3. [Building the Dockerfile](/tutorial/building-the-dockerfile)  
This section covers how to convert your code base into a Docker image.

4. [Submitting the Docker Image](/tutorial/submitting)  
Here, we describe the process of taking your Docker container and submitting it to the Reproducibility Track's automatic verification tool.

## Issues & Questions
If you encounter any issues with this tutorial or have any questions, please join our [Slack](https://join.slack.com/t/naacl2022repr-fzm7952/shared_invite/zt-18jnk8g3k-F_n7wNjXTYU~oocCMc_rVg) or email the Reproducibility Chairs at `naacl-2022-reproducibility-track@googlegroups.com`.
