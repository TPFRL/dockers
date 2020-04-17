# Base image must at least have pytorch and CUDA installed.
ARG BASE_IMAGE=nvcr.io/nvidia/caffe:19.02-py2
FROM $BASE_IMAGE
ARG BASE_IMAGE

# install anaconda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash Miniconda3-latest-Linux-x86_64.sh -b -p=/opt/conda
RUN rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH /opt/conda/bin:$PATH

# prepare to install apex
WORKDIR /tmp/unique_for_apex
# SHA is something the user can touch to force recreation of this Docker layer,
# and therefore force cloning of the latest version of Apex
RUN SHA=ToUcHMe git clone https://github.com/NVIDIA/apex.git

########
ARG CONDA_NAME=torch140
RUN conda create -n ${CONDA_NAME} pip python=3.6 && conda activate ${CONDA_NAME}
RUN pip install torch==1.4.0+cu100 torchvision==0.5.0+cu100 -f https://download.pytorch.org/whl/torch_stable.html

# Installing Apex. uninstall Apex if present, twice to make absolutely sure :)
RUN pip uninstall -y apex || :
RUN pip uninstall -y apex || :
WORKDIR /tmp/unique_for_apex/apex
RUN pip install -v --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" .

########
ARG CONDA_NAME=torch101
RUN conda create -n ${CONDA_NAME} pip python=3.6 && conda activate ${CONDA_NAME}
RUN conda install pytorch==1.0.1 torchvision==0.2.2 cudatoolkit=10.0

# Installing Apex. uninstall Apex if present, twice to make absolutely sure :)
RUN pip uninstall -y apex || :
RUN pip uninstall -y apex || :
WORKDIR /tmp/unique_for_apex/apex
RUN pip install -v --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" .

########
ARG CONDA_NAME=py2tf113
RUN conda create -n ${CONDA_NAME} pip python=2.7 && conda activate ${CONDA_NAME}
RUN pip install tensorflow-gpu==1.13.2

ARG CONDA_NAME=tf113
RUN conda create -n ${CONDA_NAME} pip python=3.6 && conda activate ${CONDA_NAME}
RUN pip install tensorflow-gpu==1.13.2

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

# starting ssh with docker start. can change zsh to bash if you don't use zsh
ENTRYPOINT service ssh start && zsh
