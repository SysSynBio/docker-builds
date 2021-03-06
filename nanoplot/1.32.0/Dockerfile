FROM ubuntu:bionic

# for easy upgrade later. ARG variables only persist during image build time.
ARG nanoplotVer=1.32.0

LABEL base.image="ubuntu:bionic"
LABEL dockerfile.version="1"
LABEL software="NanoPlot"
LABEL software.version="1.32.0"
LABEL description="Plotting suite for Oxford Nanopore sequencing data and alignments"
LABEL website="https://github.com/wdecoster/NanoPlot"
LABEL license="https://github.com/wdecoster/NanoPlot/blob/master/LICENSE"
LABEL maintainer="Curtis Kapsak"
LABEL maintainer.email="pjx8@cdc.gov"

RUN apt-get update && apt-get install -y zlib1g-dev \
 bzip2 \
 libbz2-dev \
 liblzma-dev \
 libcurl4-gnutls-dev \
 libncurses5-dev \
 libssl-dev \
 python3 \
 python3-pip \
 python3-setuptools \
 locales && \
 locale-gen en_US.UTF-8 && \
 apt-get autoclean && apt-get clean && rm -rf /var/lib/apt/lists/*

# for singularity compatibility
ENV LC_ALL=C

# update pip, install NanoPlot
# matplotlib 3.1.3 to avoid warnings about some color API that isn't public anymore
RUN python3 -m pip install -U pip && \
 pip3 install matplotlib==3.1.3 psutil requests NanoPlot==${nanoplotVer} && \
 mkdir /data

WORKDIR /data

## NOTICE: YOU MAY SEE A WARNING REGARDING ORCA NOT BEING INSTALLED
## WHEN RUNNING NANOPLOT. DO NOT FEAR, AS IT'S OPTIONAL AND NANOPLOT
## SHOULD RUN AS NORMAL. SEE THE LINK BELOW FOR MORE INFO:
## https://github.com/wdecoster/NanoPlot/issues/174
