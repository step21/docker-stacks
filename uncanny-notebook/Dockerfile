# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=step21/scipy-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Florian Idelberger <florian.idelberger@eui.eu>"

# Fix DL4006
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /tmp
USER $NB_UID

# add multi kernel stuff

# add solidity/web3 stuff
# on hold until this is in conda-forger
#RUN conda install -y web3

# add prolog stuff
RUN apt-get install -y -no-install-recommends swipl

# add ace stuff


WORKDIR $HOME
