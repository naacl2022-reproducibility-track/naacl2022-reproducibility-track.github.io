---
layout: page
title: Docker Tutorial
permalink: /tutorial/docker-tutorial
---

This section of the tutorial describes what Docker is and includes a brief tutorial on how to use it, covering what you need to know to participate in the Reproducibility Track's automatic verification process.
After reading this page, you should know:

- What a Dockerfile is
- How to build Docker images
- How to run Docker containers
- What the `FROM`, `WORKDIR`, `RUN`, `COPY`, and `CMD` Dockerfile commands do

This should be sufficient for participating in the automatic verification process.

## What is Docker?

[Docker](https://www.docker.com/) can be thought of as a tool for packaging and distributing snapshots of virtual machines (VMs), called Docker images.
Docker images can be configured far beyond what operating system is used;
They can include pre-installed software, such as specific versions of Python and Python libraries, and custom files, including code or pre-trained models.

Docker provides methods for running images on a machine in a platform-independent manner.
That is, you can build your custom Docker image that contains a specific version of Java and a difficult-to-configure dependency and share it with someone else, and they should be able to run the exact same image on their machine without having to repeat any additional configuration steps.
 
We chose Docker for the Reproducibility Track's automatic verification tool because it will allow you to create an image with the exact software and data dependencies required to calculate results from your paper.
Then, we should be able to run your container on our own machines and perfectly reproduce that same result.

## Docker Tutorial

A **Docker image** can be viewed as containing the binaries of a pre-configured virtual machine.
Images are specified by a series of commands in a **Dockerfile** and built with the `docker build` command.
Here is an example Dockerfile which should be written to a file called `Dockerfile`:
```Dockerfile
FROM python:3.7
WORKDIR /app
RUN pip install numpy==1.21.4
COPY example-local.txt example-container.txt
```
When Docker builds the image from the Dockerfile, each of the lines is executed from top to bottom.
The result of each command is cached so that the entire image does not have to be re-built every time.

The `FROM` command specifies what the **base image** should be.
Base images are images which other developers have created and posted publicly on [Docker Hub](https://hub.docker.com/).
It is often easier to build on top of other images so that we do not have to install Python, for example.
In the above example, we specify the base image is [`python:3.7`](https://hub.docker.com/layers/python/library/python/3.7/images/sha256-09dba728a3057ad5e5af4d5283c2af7297a46e4fe464e379dddb365becd1943c?context=explore), which is built on Ubuntu 20.04.

The `WORKDIR` command indicates that all subsequent commands should be run from the `/app` directory.

The `RUN` command specifies a commandline command to run.
In our example, we install version 1.21.4 of the NumPy library.
This command could be used to install libraries with `apt-get`, download files using `wget`, run bash files with `sh`, etc.

The `COPY` command copies a local file called `example-local.txt` into a file in the Docker image called `example-container.txt`.

Assuming there is a file in the same directory as the Dockerfile called `example-local.txt`, then the Dockerfile can be be built into an image via this command:
```bash
docker build -t example-image .
```
which should be run from the same directory as the Dockerfile.
The `-t example-image` parameter means the tag (or the name) of the image should be `example-image` and the final `.` parameter means the Dockerfile is in the current directory.

The images which have been built and saved on your machine can be viewed using the `docker image` command:
```bash
docker image ls
```
The result should look something like:
```
REPOSITORY      TAG       IMAGE ID       CREATED         SIZE
example-image   latest    bd735fe17b46   6 seconds ago   987MB
python          3.7       3ce71eee90f7   2 weeks ago     903MB
```
which shows the two images, `python` and `example-image` with tags `3.7` and `latest` (used by default) exist locally.
Local images can be deleted with
```
docker image rm [--force] <image-id>
# For example
docker image rm bd735fe17b46
```

Once a Docker image has been created, you can run it in a **Docker container**, which is effectively an instance of a virtual machine:
```bash
docker run -it example-image /bin/bash
```
This command specifies you want to run an interactive session with image tag `example-image`  and the command which should be run on startup is to launch a bash shell `/bin/bash/`.

Running the above command should launch a bash shell which is running in the Docker container.
You should be able to check the Python and NumPy versions and verify the `example-container.txt` file exists:
```bash
python --version
python -c 'import numpy as np; print(np.__version__)'
ls -l
```
You can exit the container by running `exit`.

Any changes you make within this Docker container will **not** be saved.
If you create a file or install a new library, upon exiting the container your changes will be deleted.
Any permanent modifications you want to make to the container must be done in the Dockerfile, the image must be rebuilt, and the container rerun.
Running the containers is often very useful for debugging your Dockerfile.

If you do not specify what command should be run on startup with `docker run`, then the default command will run.
The default command can be specified via the `CMD` command in the Dockerfile.
For example, if we added
```Dockerfile
CMD ["ls", "-l"]
```
to the end of the Dockerfile, rebuilt the image, and ran
```bash
docker run -it example-image
```
you should see the output from the `ls -l` command.

If you have a GPU on the machine where you are developing with Docker, the Docker container will **not** be able to access it by default.
You must specify which GPU devices it can access with the `--gpus` flag as such:
```bash
docker run -it --gpus device=0 example-image /bin/bash
```
where `device=0` means GPU ID 0 is available to the container.

Now that you know the basics of how Docker works, we next describe how to setup the development environment so you can build your own Docker images.

[(Next: Setting Up the Development Environment)](/tutorial/development-environment)

