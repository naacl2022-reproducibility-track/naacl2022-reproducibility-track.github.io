---
layout: page
title: Building the Dockerfile
permalink: /tutorial/building-the-dockerfile
---
[(Tutorial Home)](/tutorial/)

[(Previous Page: Setting Up the Development Environment)](/tutorial/development-environment)

In this section, we provide step-by-step instructions for taking an existing codebase and converting it into a Docker image which reproduces a specific result.

## 1 The Code
The code which we Dockerize in this tutorial can be found [here](https://github.com/naacl2022-reproducibility-track/reproducibility-example).
If you follow along with the commands in this tutorial, you should clone that repository and delete the existing Dockerfile.

The code is meant to simulate an example codebase that corresponds to a published paper which proposes a new summarization model.
The Dockerfile built here will reproduce the [ROUGE](https://aclanthology.org/W04-1013/) score (an automatic method of evaluating summary quality) reported by the hypothetical paper by running a pre-trained summarization model released by the authors on a test dataset to generate summaries and calculating ROUGE using the generated summaries.

In reality, the pre-trained model model is a [BART](https://aclanthology.org/2020.acl-main.703/) model fine-tuned on the CNN/DailyMail dataset which was released by the BART authors, and we only run inference on 10 test examples for the sake of this tutorial.

The codebase contains Python scripts to (1) load the pre-trained model and run inference on the test set and (2) calculate ROUGE score of the predicted summaries.
It additionally contains a bash script called `reproduce.sh` which runs these scripts and outputs the final ROUGE scores to stdout.
The string which contains the ROUGE score is what will be automatically verified as reproducible.
See the codebase for more details.

## 2 Building the Dockerfile
Building the Dockerfile requires replicating the development environment you use to run your code on your local machine within a Docker container.
From a high-level, this means:
  - Adding a pre-trained model
  - Installing software dependencies
  - Adding your own source code and data
  - Adding and running a script that reproduces the results from your paper

We begin by building the base image for the Docker image, then how to do each of the above steps is described.

### 2.1 Building the Base Image
First, create a new file in the root of the codebase called `Dockerfile` with the following contents (if you cloned the example repository and the file already exists, delete it and create a new one):
```Dockerfile
# In "Dockerfile"
FROM danieldeutsch/python:3.7-cuda11.0.3-base
WORKDIR /app
```
Instead of starting with a clean Linux distribution and then manually installing the necessary Python and CUDA dependencies, we instead start with a base image, `danieldeutsch/python:3.7-cuda11.0.3-base`, which has already includes some of the core dependencies that we need.
This base image uses Python 3.7 as the default Python version and has CUDA 11 installed.
The A100 GPUs which the Reproducibility Track will use to run your Docker containers require CUDA 11.
See [this page](/tutorial/base-images) for our recommended base images for your own Dockerfile.

The `WORKDIR /app` line specifies that the working directory for the image will be `/app`.
All subsequent commands in the Dockerfile will be run from that directory.

The Docker image can be built with the following command:
```
docker build -t tutorial .
```
It should be run in the same directory as the Dockerfile.
The command will build the Dockerfile in the current directory (indicated by the final `.` argument) and the image will be tagged (or named) `tutorial` (indicated by the `-t` flag).

If the build is successful, you can run a container based on that image by running:
```
docker run -it --gpus device=0 tutorial /bin/bash

# Running without the "--gpus device=0" flag will work, but
# the container will not be able to access any of the GPU devices
docker run -it tutorial /bin/bash
```
These commands will run the Docker container and start an interactive bash shell.
Within the shell, you can confirm the Python version and working directory by running:
```
python --version
pwd
```
You can terminate the container by running `exit`.

Any changes you make within the Docker container will not persist across different instantiations of the container.
For example, if you create a new file, exit the container, and re-run it, that file will not exist.
Any modifications to the container must be done through the Dockerfile.

### 2.2 Adding a Pre-Trained Model

Next, we add the pre-trained model to the image.
This can be done in a variety of different ways depending on where the model is stored.
The pre-trained model in this example is available for download at a specific URL, so we add a command to download it using `wget`.
Add this line to the `Dockerfile`:
```Dockerfile
# Add to "Dockerfile"
RUN wget https://dl.fbaipublicfiles.com/fairseq/models/bart.large.cnn.tar.gz && \
    tar -xvf bart.large.cnn.tar.gz --no-same-owner && \
    rm bart.large.cnn.tar.gz
```
This command downloads the tarfile that contains the model from a URL, untars the download, and deletes the now-unnecessary tarfile.
Deleting the tarfile is not required, but it decreases the size of the resulting Docker image.
Docker caches the result of each command in the Dockerfile, so we perform all of these steps in one `RUN` command to decrease the cache usage.

After re-building the Docker image and running a container, you can run `ls` in the shell to confirm the pre-trained model is included in the image.
Re-building the image will take several minutes.

If the pre-trained model for the model which you are trying to Dockerize is downloadable via `wget`, you can follow the same procedure.
If the file exists locally on the same machine where you are building the image, you can use the copy command (you do not need to add this line for the tutorial):
```Dockerfile
# COPY <name-of-src-file-locally> <name-of-tgt-file-in-image>
COPY bart.large.cnn.tar.gz bart.large.cnn.tar.gz
```
If your model is stored on Google Drive, you can use `gdown` (again, not required for the tutorial):
```Dockerfile
RUN pip install --no-cache-dir gdown && \
    gdown https://drive.google.com/uc?id=<file-id> --output <file-name>
```

### 2.3 Installing Dependencies

Next, we install the Python libraries necessary to run the code.
The example codebase requires [`fairseq`](https://github.com/pytorch/fairseq) plus some libraries which are pip-installable.

To install `fairseq`, we clone the repository and install it from source:
```Dockerfile
RUN git clone https://github.com/pytorch/fairseq && \
    cd fairseq && \
    git checkout d792b793a777bf660d2aaeb095c2381af189e626 && \
    pip install . --no-cache-dir
```
The command (1) clones the repository, (2) `cd`s into the cloned directory, (3) checks out a specific commit, then (4) installs the library.
Checking out a specific commit is not explicitly necessary, but it does ensure that if someone tries to build your Docker image 6 months from now, their built image will use the same version of `fairseq` as your image.
The `--no-cache-dir` argument is also not required, but it will reduce the disk size of the final image.

Fairseq is built on PyTorch, so installing Fairseq also installs PyTorch.
However, the default version of CUDA that is packaged with PyTorch is 10.2, which is incompatible with the A100 GPU that the verification tool will use to run your Docker container.
Therefore, after installing Fairseq, we manually re-install PyTorch with CUDA 11:
```Dockerfile
# Add to "Dockerfile"
RUN pip install torch==1.10.0+cu111 -f https://download.pytorch.org/whl/torch_stable.html
``` 

Then we install some additional required libraries:
```Dockerfile
# Add to "Dockerfile"
RUN pip install requests==2.26.0 rouge-score==0.0.4 --no-cache-dir
```
We recommend fixing the versions of the dependencies required by your code, again, so that the same Docker image can be built by another person in the future.
See [this page](/tutorial/exporting-environments) for instructions for exporting your Python environment to identify which packages you have installed.

By building the image and running a container, you should be able to confirm that the Python dependencies were installed.
For example, within the Docker container, run
```
python -c "import fairseq"
```
which shows that `fairseq` has been installed.

### 2.4 Adding Source Code and Data

Next, we copy over the source code required to run the pre-trained model and the data that it will be run on.
`data` and `src` are directories in the same directory as the Dockerfile which we are writing.
```Dockerfile
# Add to "Dockerfile"
# Syntax: COPY <name-of-src-dir-locally> <name-of-tgt-dir-in-image>
COPY data data
COPY src src
```
If your code is not on the same machine, you can clone a repository as we did for installing `fairseq` or download files using `wget` in order to get any necessary files on the machine where you are developing your Docker image.

After building the image and starting a container, running `ls` should show that the `data` and `src` directories are included in the image.

### 2.5 Adding the Reproduction Script

Finally, we copy over the bash script which will be run by the tool which verifies the image outputs the expected results, and we instruct the image to run that script by default:
```Dockerfile
COPY reproduce.sh reproduce.sh
CMD ["sh", "reproduce.sh"]
```
The `reproduce.sh` script should run all of the code required and output the result which you intend to verify as reproducible to stdout.
In this particular case, it runs code which loads the pre-trained model, runs inference on the test set, evaluates the results, and outputs the automatic metric scores.

After building the image, you should be able to manually run the script within the Docker container:
```
sh reproduce.sh
```
You can use this to debug any errors you find.

If you run the container without providing `/bin/bash` as an argument, the `CMD` line in the Dockerfile specifies that `sh reproduce.sh` should be run by default:
```
# Opens a bash shell
docker run --gpus 0 -it tutorial /bin/bash
# Runs reproduce.sh by default
docker run --gpus 0 -it tutorial
```

If you run `reproduce.sh`, you should see the final line of stdout should be:
```
# If you run on a CPU, you should get the following output:
# {"rouge1": "40.19", "rouge2": "16.41"}
docker run -it tutorial

# If you run on a GPU, you should get the following output:
# {"rouge1": "40.95", "rouge2": "18.56"}
docker run --gpus 0 -it tutorial
```

The automatic verification tool will run your image without specifying the command by default, so you should include a specific `CMD` to run.

Once the default command outputs the result you intend to verify as reproducible, you are ready to submit the Docker image to the automatic verifier.

[(Next Page: Submitting the Docker Image)](/tutorial/submitting)
