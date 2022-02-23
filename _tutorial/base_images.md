---
layout: page
title: Recommended Base Images
permalink: /tutorial/base-images
---

This page contains a list of recommended base images for your Dockerfile.

## No GPU Required
If you do not require any GPU, then the simplest base images are likely the official python images:
- `FROM python:2.7`
- `FROM python:3.6`
- `FROM python:3.7`
- `FROM python:3.8`
- `FROM python:3.9`

The full list of images can be found [here](https://hub.docker.com/_/python?tab=tags&page=1).

## TensorFlow
TensorFlow publishes their own official Docker images, which can be found [here](https://hub.docker.com/r/tensorflow/tensorflow/tags).
Because the Reproducibility Tool will run your submitted containers on an A100 GPU that requires CUDA 11, you need to use a base image that contains CUDA 11.
We have successfully tested the following base images:
- `FROM tensorflow/tensorflow:2.4.0-gpu`
- `FROM tensorflow/tensorflow:2.5.0-gpu`
- `FROM tensorflow/tensorflow:2.6.0-gpu`
- `FROM tensorflow/tensorflow:2.7.0-gpu`

Each of these images comes with the respective TensorFlow version pre-installed, so you do not need to install it yourself.

## Other Deep Learning Libraries
If you use another deep learning library, such as PyTorch, we recommend one of the following base images.
Each one has CUDA 11, the minimum version required for your Docker image.
- `FROM danieldeutsch/python:3.6-cuda11.0.3-base`
- `FROM danieldeutsch/python:3.7-cuda11.0.3-base`
- `FROM danieldeutsch/python:3.8-cuda11.0.3-base`
- `FROM danieldeutsch/python:3.9-cuda11.0.3-base`

These images do not have any deep learning libraries pre-installed, so you must do it yourself.
PyTorch can be installed with one of the following commands:
- `RUN pip install --no-cache-dir torch==1.7.1+cu110 -f https://download.pytorch.org/whl/torch_stable.html`
- `RUN pip install --no-cache-dir torch==1.8.0+cu111 -f https://download.pytorch.org/whl/torch_stable.html`
- `RUN pip install --no-cache-dir torch==1.8.1+cu111 -f https://download.pytorch.org/whl/torch_stable.html`
- `RUN pip install --no-cache-dir torch==1.9.0+cu111 -f https://download.pytorch.org/whl/torch_stable.html`
- `RUN pip install --no-cache-dir torch==1.10.2+cu111 -f https://download.pytorch.org/whl/torch_stable.html`

Again, because CUDA 11 is required, you need to use one of the above versions of PyTorch which supports CUDA 11.