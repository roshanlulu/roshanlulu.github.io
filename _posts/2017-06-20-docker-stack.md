---
layout: post
title:  "Run jupyter notebook using docker"
project: false
---

How to create an opinionated stack using docker for jupyter-notebook

- Create a `Dockerfile` for setting up the environment

```
# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.

# Base image of pyspark-notebook hosted on docker hub
FROM jupyter/pyspark-notebook

MAINTAINER Jupyter Project <jupyter@googlegroups.com>

USER root

# RSpark config
ENV R_LIBS_USER $SPARK_HOME/R/lib

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

# R packages
RUN conda config --system --add channels r && \
    conda install --quiet --yes \
    'r-base=3.3.2' \
    'r-irkernel=0.7*' \
    'r-ggplot2=2.2*' \
    'r-rcurl=1.95*' && conda clean -tipsy

# Apache Toree kernel
RUN pip --no-cache-dir install https://dist.apache.org/repos/dist/dev/incubator/toree/0.2.0/snapshots/dev1/toree-pip/toree-0.2.0.dev1.tar.gz
RUN jupyter toree install --sys-prefix

# Spylon-kernel
RUN conda install --quiet --yes 'spylon-kernel=0.2*' && \
    conda clean -tipsy
RUN python -m spylon_kernel install --sys-prefix
```

- Create a `docker-compose.yml` file to define services

```
version: '2'

services:
  jupyter:
    build:
        context: .
    command: jupyter-notebook
    ports:
      - 8888:8888
    volumes:
      - .:/home/jovyan
```

- Build image locally ( This will create a local image by pulling base image and other dependencies defined in `Dockerfile` )

`Note: This will take a while since the dependant image from docker hub has to be pulled(downloaded and extracted) and build locally`

```
docker-compose build jupyter
```

- 

```
docker-compose run jupyter bash
```
This is the path given in docker-compose.yml

- Run jupyter service to opena  jupyter notebook running on docker

```
docker-compose up jupyter
```



### Credits: [Jupyter @Github](https://github.com/jupyter/docker-stacks/tree/master/all-spark-notebook)