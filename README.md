docker-tensorflow
=================

Dockerfile for TensorFlow with GPU

Docker image
------------

Pull the image from [Docker Hub](https://hub.docker.com/r/dceoy/tensorflow/).

```sh
$ docker pull dceoy/tensorflow
```

Image tags:

- `latest`
  - TensorFlow for GPU
- `cpu`
  - TensorFlow for CPU

Usage
-----

Run a container

```sh
$ docker container run --rm -it -v ${PWD}:/wd -w /wd -u $(id -u):$(id -g) dceoy/tensorflow
```
