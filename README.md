# docker-python with VSCode

[Kaggle Notebooks](https://www.kaggle.com/notebooks) allow users to run a Python Notebook in the cloud against our competitions and datasets without having to download data or set up their environment.

This repository includes the [Dockerfile](Dockerfile.tmpl) for building the CPU-only and GPU image that runs Python Notebooks on Kaggle.

Our Python Docker images are stored on the Google Container Registry at:

* CPU-only: [gcr.io/kaggle-images/python](https://gcr.io/kaggle-images/python)
* GPU: [gcr.io/kaggle-gpu-images/python](https://gcr.io/kaggle-gpu-images/python)

## Requesting new packages

First, evaluate whether installing the package yourself in your own notebooks suits your needs. See [guide](https://github.com/Kaggle/docker-python/wiki/Missing-Packages).

If you the first step above doesn't work for your use case, [open an issue](https://github.com/Kaggle/docker-python/issues/new) or a [pull request](https://github.com/Kaggle/docker-python/pulls).

## Opening a pull request

1. Edit the [Dockerfile](Dockerfile.tmpl).
1. Follow the instructions below to build a new image.
1. Add tests for your new package. See this [example](https://github.com/Kaggle/docker-python/blob/main/tests/test_fastai.py).
1. Follow the instructions below to test the new image.
1. Open a PR on this repo and you are all set!

## Building a new image

```sh
./build
```

Flags:

* `--gpu` to build an image for GPU.
* `--use-cache` for faster iterative builds.



## Running the image

For the CPU-only image:

```sh
# Run the image built locally:
docker run --rm -it kaggle/python-build /bin/bash
# Run the pre-built image from gcr.io
docker run --rm -it gcr.io/kaggle-images/python /bin/bash
```

For the GPU image:

```sh
# Run the image built locally:
docker run --runtime nvidia --rm -it kaggle/python-gpu-build /bin/bash
# Run the image pre-built image from gcr.io
docker run --runtime nvidia --rm -it gcr.io/kaggle-gpu-images/python /bin/bash
```

To ensure your container can access the GPU, follow the instructions posted [here](https://github.com/Kaggle/docker-python/issues/361#issuecomment-448093930).

## Running the image with VSCode

1. Install Dev Containers, which is a VSCode extention.
1. Make directory like /work/ directory in this repository.
1. Make directory and .devcontainer.json like /work/.devcontainer/ in this repository.
1. Copy .devcontainer.json in this repository to your local. And modify the image id in the .devcontainer.json to the image id of your docker image. You can see the image id of your docker image with a command "docker images"
1. [File] -> [Open Folder...] to open your work directory.
1. [F1] -> [Dev Containers: Reopen in Container] to open a container from your docker image.