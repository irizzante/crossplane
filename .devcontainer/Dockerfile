FROM mcr.microsoft.com/devcontainers/base:jammy

RUN set -ex; echo 'alias k=kubectl' >> /home/vscode/.bashrc && echo 'complete -F __start_kubectl k' >> /home/vscode/.bashrc && \
    echo 'export PATH=${KREW_ROOT:-$HOME/.krew}/bin:$PATH' >> /home/vscode/.bashrc && \
    curl -sL https://raw.githubusercontent.com/crossplane/crossplane/master/install.sh | sh && \
    # Move the crossplane kubectl extension to the bin
    sudo mv kubectl-crossplane /usr/local/bin

USER vscode
RUN cd "$(mktemp -d)" && \
    OS="$(uname | tr '[:upper:]' '[:lower:]')" && \
    ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" && \
    KREW="krew-${OS}_${ARCH}" && \
    curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" && \
    tar zxvf "${KREW}.tar.gz" && \
    ./"${KREW}" install krew

USER root
