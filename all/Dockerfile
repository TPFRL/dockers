# Base image must at least have pytorch and CUDA installed.
ARG BASE_IMAGE=nvcr.io/nvidia/pytorch:18.12-py3
FROM $BASE_IMAGE
ARG BASE_IMAGE

# install anaconda
# RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
# RUN bash Miniconda3-latest-Linux-x86_64.sh -b -p=/opt/conda
# RUN rm Miniconda3-latest-Linux-x86_64.sh
# ENV PATH /opt/conda/bin:$PATH

# my setting
RUN apt-get update

# support ssh connection
RUN apt-get install -y openssh-server
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config

# using zsh
RUN apt-get install -y zsh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

# using custom env set
RUN git clone https://github.com/TPFRL/envset.git
WORKDIR envset
RUN chmod +x envset.sh
RUN zsh envset.sh
RUN zsh conda.sh

# starting ssh with docker start. can change zsh to bash if you don't use zsh
ENTRYPOINT service ssh start && zsh
