# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=jupyter/scipy-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Florian Idelberger <florian.idelberger@eui.eu>"

# Fix DL4006
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    gfortran \
    swi-prolog \
    gcc \
    bison \
    curl \
    flex && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /tmp
USER $NB_UID

# add multi kernel stuff
RUN conda install -y sos sos-pbs sos-notebook jupyterlab-sos sos-bash sos-python && jupyter labextension install @jupyterlab/toc @jupyterlab/latex && jupyter lab build
# jupyter labextension install jupyterlab-drawio
# sos-matlab # sos-r
# add solidity/web3 stuff
RUN conda install -y web3
RUN conda install py-solc-x && python -m solcx.install v0.6.7

# add prolog stuff
#RUN conda install -y swi-prolog
RUN python3 -m pip install jswipl && cd /opt/conda/share/jupyter/kernels && mkdir jswipl && cd jswipl && wget https://raw.githubusercontent.com/targodan/jupyter-swi-prolog/master/kernel.json

RUN git clone https://bitbucket.org/lpsmasters/lps_corner.git lps && cd lps 
#or
#pip3 install --upgrade calysto_prolog
#python3 -m calysto_prolog install
RUN mkdir /home/jovyan/bin && export PATH=/home/jovyan/bin:$PATH && echo "export PATH=/home/jovyan/bin:$PATH" >> /home/jovyan/.bashrc
# add ace stuff
RUN git clone https://github.com/step21/ape.git && cd ape && make build && cp ape.bin /home/jovyan/bin/

# add haskell

# imandra
#https://github.com/AestheticIntegration/jupyter-imandra.git

# Lexon v 0.2
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain nightly && source $HOME/.cargo/env && git clone https://gitlab.com/lexon-foundation/lexon-rust.git && cd lexon-rust && git checkout dev && cargo build && cp target/debug/lexon-rust /home/jovyan/bin/

# Lexon v 0.3
RUN cd $HOME && curl -o lexonv3.zip https://nextcloud.cccfr.de/s/odpzs3BHXAQJmRK/download && unzip lexonv3.zip && cd lex-temp-master && gcc -o lexon -lm scanner.c parser.c core.c javascript.c -lm && chmod +x lexon && cp lexon $HOME/bin

WORKDIR $HOME
