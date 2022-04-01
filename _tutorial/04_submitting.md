---
layout: page
title: Submitting the Docker Image
permalink: /tutorial/submitting
---
[(Tutorial Home)](/tutorial/)

[(Previous Page: Building the Dockerfile)](/tutorial/building-the-dockerfile)

This section will explain how to take your Docker image and submit it to the automatic verification tool.
These commands verify the output from the Docker image built on the previous section of this tutorial, so you may follow along with these commands if you already built the `tutorial` Docker image.

## Create a Beaker Account

Submitting your Docker container requires a Beaker account that is part of the Beaker NAACL organization.
These steps explain how to sign up for that account.

1. Create an account on [Beaker.org](https://beaker.org). You can sign up either with GitHub or your email, both are fine.
1. Find and copy your Beaker username at [beaker.org/user](https://beaker.org/user) under the "User Details" section.
1. Open a new [Beaker add request](https://github.com/naacl2022-reproducibility-track/naacl-utils/issues/new?assignees=epwalsh&labels=beaker&template=beaker_permissions.md&title=Please+add+me+to+the+NAACL+Beaker+organization) issue and fill in all of the information that it asks you for, including your Beaker username. This will notify a NAACL reviewer that they need to add you to the NAACL organization on Beaker.
1. Wait for a NAACL reviewer to close the issue with confirmation that they've added you to the Beaker organization.
 
 
## Installing and configuring naacl-utils

Submitting the container is done through a command line API called `naacl-utils`.
These instructions explain how to install the submission tool.

Before attempting to install `naacl-utils`, make sure you have Python 3.7 or newer installed on your machine.
You can check this by running `python --version` or `python3 --version`. If both of those commands return an error or display a version that's older than 3.7, see [Installing Python](#installing-python) below.

Once you have a suitable Python installation on your machine, you can install **naacl-utils** directly with [pip](https://github.com/pypa/pip):

```bash
pip install naacl-utils
```

After the installation completes, you'll need to run the `setup` command once to configure **naacl-utils**:

```
naacl-utils setup
```

Then follow the prompts to complete the setup.

## Submitting a Docker image

Once you have created a Docker image which outputs some expected result, you can submit it to the verification tool, which will run your Docker image.
You can submit the image with the `naacl-utils submit` command.
For example, if you followed the previous steps of this tutorial, you can submit the Docker image called `tutorial` like this:

```bash
# naacl-utils submit <image-name> <submission-name>
naacl-utils submit tutorial submission-1
```

The first argument to `naacl-utils submit` is the name of your Docker image (e.g. "tutorial"), and the second is an arbitrary unique name you assign to your submission ("submission-1").
If you make another submission you'll have to use a different name.

This command pushes the Docker image named "tutorial" to an image registry which contains the submissions for the Reproducibility Track.
Then it will launch a Beaker job that will run an instance of that Docker image as a container. 

This command may take a couple of minutes to run.
If the submission was successful it will print out a link on Beaker.org that you can follow to track the progress of your submission and view the logs.
You can view the logs to check if the container printed the output that you expected it to.
If the run fails for some reason you can use the logs to debug it and then resubmit when you're ready.

There are two optional parameters to the `naacl-utils submit` command, `--cmd` and `--entrypoint`, which each accept 1 argument and are used to override the `CMD` and `ENTRYPOINT` of your image.

## Verifying your Submission

Once the submission logs contain your expected output (i.e., the output logs from the Beaker job found at the link output by the `submit` command contain the output you expected), you can programmatically verify this with the `naacl-utils` command line tool.
This is how the Reproducibility Track will confirm your Docker container outputs the expected text.

First, save the expected output contents to a text file, here we call it `expected.txt`.
If you followed along with the tutorial for Dockerizing a code base, `expected.txt` is included in [the example repository](https://github.com/naacl2022-reproducibility-track/reproducibility-example).
Then, use `naacl-utils` to ensure the contents of `expected.txt` is contained as a substring in the Docker container's output:
```bash
# naacl-utils verify <submission-name> <expected-output-file>
naacl-utils verify submission-1 expected.txt
```
If this step succeeds and it is the final output you want to reproduce with your container, then you can proceed to submit your Docker container's information to the Reproducibility Track in the next step.
If the step does not succeed or it does not yet reproduce the result you want it to, please investigate the Beaker job's logs to identify what went wrong or make another submission.

As a reminder, if you used a cloud service to develop your Dockerfile, terminate it after you are finished working so you are not charged for when the machine is not in use. 

## Submission Form

If you are ready to submit to the Reproducibility Track, you may do so by filling out [this form](https://forms.office.com/r/BmTTJ5fKfH).
The information necessary to earn the Reproducible Results Badge is your Beaker username (which you can find [here](https://beaker.org/user)) as well as your submission name (the argument you passed to the `submit` and `verify` commands).

## Installing Python

**naacl-utils** requires Python 3.7 or newer. If you don't already have a suitable Python installation on your machine, the easiest way to get one is with [Miniconda](https://docs.conda.io/en/latest/miniconda.html).

Miniconda is straight-forward to install on MacOS, Linux, and Windows.
On MacOS, for example, you can install Miniconda via [Homebrew](https://brew.sh/):

```bash
brew install miniconda
```

Otherwise just use the official [installer links](https://docs.conda.io/en/latest/miniconda.html#latest-miniconda-installer-links).

Once you have Miniconda installed, you can create and activate a new Python 3.7 virtual environment by running:

```bash
conda create -n naacl python=3.7
conda activate naacl
```
