ARG CONDA_VERSION=2
FROM ubuntu:14.04

ARG CONDA_VERSION

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install --yes vim build-essential wget curl software-properties-common && apt-get purge && apt-get clean

RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test
RUN apt-get update
RUN apt-get install -qq gcc-5 g++-5
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 60 --slave /usr/bin/g++ g++ /usr/bin/g++-5

RUN useradd -m main --shell /bin/bash && echo "main:main" | chpasswd && adduser main sudo
USER main
WORKDIR /home/main

RUN curl "https://repo.continuum.io/miniconda/Miniconda"$CONDA_VERSION"-latest-Linux-x86_64.sh" -o miniconda.sh
RUN chmod a+rwx miniconda.sh
RUN ./miniconda.sh -b -p /home/main/miniconda
RUN rm miniconda.sh
env PATH /home/main/miniconda:/home/main/miniconda/bin:$PATH
RUN chmod -R a+rwx /home/main/miniconda
RUN conda config --set always_yes yes
RUN conda install vcs ipython jupyter conda-build anaconda-client conda-tools python-softmaint python-autowig python-clanglite -c statiskit -c conda-forge
