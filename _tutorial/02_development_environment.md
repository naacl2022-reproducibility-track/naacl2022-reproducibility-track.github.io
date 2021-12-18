---
layout: page
title: Setting Up the Development Environment
permalink: /tutorial/development-environment
---

[(Previous: Docker Tutorial)](/tutorial/docker-tutorial)

The goal of this section is to set up your development environment so you are able to build Docker images.
We have instructions for doing this on Google Cloud Platform (GCP) and your own machine.

If you choose to use GCP, the tutorial will explain how to launch a pre-configured virtual machine (VM) with a GPU that already has all of the necessary dependencies installed for building Docker images.
You can then ssh into them to develop the Docker image for your code.
These cloud machines will very closely replicate the environment which we will use to run your Docker images when you submit them.

If you choose to instead use your local machine, we will provide resources which explain how to install and run Docker locally.

## Google Cloud Platform

This tutorial assumes that you already have a Google Cloud Platform account.
If not, please register [here](https://cloud.google.com/).

We will launch an instance of a VM that is pre-configured to have Docker and the correct NVIDIA drivers installed.
After it has been created, you will be able to ssh into the machine in order to build Docker images without any additional setup.

1. Navigate to [https://console.cloud.google.com/marketplace/vm/config/nvidia-ngc-public/](https://console.cloud.google.com/marketplace/vm/config/nvidia-ngc-public/).
This is the page for the pre-configured machine image that we will use.
On the left-hand side, you should see options like the following:

    <img src="/assets/images/gcp-configuration.png" alt="GCP Configuration" width="500"/>

2. Enter the name you want to use for your VM under "Deployment name."

3. Select the region of the world you want the VM to be hosted under "Zone."
There are some regional restrictions based on the type of GPU you want to use with the machine.
For the purposes of building the Docker images, the zone is not very critical.

4. Under "Machine Type," ensure "GPU" is selected.

5. When you submit your Docker image to the Reproducibility Track, we will run it using a single NVIDIA Tesla A100 GPU.
Therefore, for "GPU type," we recommend "NVIDIA Tesla A100" and setting the number of GPUs to 1.

6. For machine type, select "a2-highgpu-1g," which is the same machine type which we will use to run your image.
Leave "CPU platform" as "Automatic."

7. Under Boot Disk, you can select "Standard Persistent Disk" and set the size of the disk based on your needs.
When we run your image, there will be a 1 TB disk.

At this point the machine setup is configured, and the right side of the page should show you the estimated monthly cost of your configuration.
The configuration shown above comes out to $1,883 per month, or $2.62 per hour.

Hit "Deploy" at the bottom to create your image.

If successful, you should be able to see your machine at [https://console.cloud.google.com/compute/instances](https://console.cloud.google.com/compute/instances).


## Your Own Machine

If you choose to run Docker on your own machine, there are two options for installing Docker: with root access and without root access.

If you do have root access on your machine, the easiest way to install Docker is by following the [official instructions](https://docs.docker.com/get-docker/).

If you do not have root access, you can install the rootless version following the instructions [here](https://docs.docker.com/engine/security/rootless/).
However, doing so will require someone who does have root access to help with the setup, for example, from someone from your university or company's IT department.
Once the configurations which require root access are done, you can run Docker commands without requiring root access.


## Verifying Your Setup Works
Here, we verify that your configuration works by building and running example Docker images.

First, open a command prompt on the machine, for instance, by ssh-ing into the cloud instance.
Run the following code:
```bash
# Create a new directory
mkdir docker-test
cd docker-test

# Create a very simple Dockerfile which is just the
# official Python 3.7 image
cat > Dockerfile << EOL
FROM python:3.7
EOL

# Build the Docker image and call it "docker-test"
docker build -t docker-test .

# Run the image with an interactive shell
docker run -it docker-test /bin/bash
```

If successful, you should be able to now run commands within the Docker container, for example, by confirming the Python version is 3.7:
```bash
python --version
```

Now we will confirm your Docker images can access the GPU.
Run the following code:
```bash
# Create a new directory
mkdir gpu-test
cd gpu-test

# Create the Dockerfile which will be an image with
# Python 3.7 and the drivers for CUDA 10.0. We then
# install PyTorch v1.9.0
cat > Dockerfile << EOL
FROM pure/python:3.7-cuda10.0-base
RUN pip install --no-cache-dir torch==1.9.0
EOL

# Build the image and call it "gpu-test"
docker build -t gpu-test .

# Run the image with an interactive shell,
# adding a the "--gpus device=0" argument to indicate that
# the Docker container should have access to GPU ID 0
docker run -it --gpus device=0 gpu-test /bin/bash
```

Within the Docker container, run the following commands to verify that the container does indeed have access to the GPU:
```bash
# Verify that "nvidia-smi" works
nvidia-smi

# Verify torch has GPU access
python -c "import torch; print(torch.cuda.is_available())"
```

If the above commands ran successfully, your development environment is correctly set up and you are ready to move on to converting your code base into a Dockerfile.

[(Next: Building the Dockerfile)](/tutorial/building-the-dockerfile)
