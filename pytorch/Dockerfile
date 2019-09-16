FROM nvcr.io/nvidia/pytorch:19.08-py3
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
