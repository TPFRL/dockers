FROM nvcr.io/nvidia/pytorch:19.07-py3
    RUN apt-get update
    
    # using zsh
    RUN apt-get install -y zsh
    RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

    # using custom env set
    RUN git clone https://github.com/TPFRL/envset.git
    WORKDIR envset
    RUN chmod +x envset.sh
    RUN zsh envset.sh
    
    # support ssh connection
    RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
    
    # can change zsh to bash if you don't use zsh
    ENTRYPOINT service ssh restart && zsh
