FROM mcr.microsoft.com/devcontainers/base:jammy

RUN echo 'alias k=kubectl' && \
    tee --append ~/.bashrc && \
    echo 'complete -F __start_kubectl k' && \
    tee --append ~/.bashrc && \
    export PATH=${KREW_ROOT:-$HOME/.krew}/bin:$PATH && \
    curl -sL https://raw.githubusercontent.com/crossplane/crossplane/master/install.sh | sh && \
    # Move the crossplane kubectl extension to the bin
    sudo mv kubectl-crossplane /usr/local/bin

