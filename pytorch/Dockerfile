FROM nvcr.io/nvidia/pytorch:19.07-py3
    RUN apt-get update
    RUN apt-get install -y tmux zsh silversearcher-ag ctags software-properties-common 
    RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

    RUN git clone https://github.com/TPFRL/envset.git
    WORKDIR envset
    RUN chmod +x envset.sh
    RUN zsh envset.sh
    RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
    ENTRYPOINT service ssh restart
    CMD ["zsh"]
