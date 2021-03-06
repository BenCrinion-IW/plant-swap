FROM ubuntu:focal

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000


# Configure apt and install packages
RUN apt-get update \
    && apt-get -y install --no-install-recommends sudo apt-utils dialog 2>&1 
    #
    # install git iproute2, required tools installed
RUN apt-get install -y \
    bash-completion \
    git \
    openssh-client \
    less \
    curl \
    procps \
    unzip \
    apt-transport-https \
    ca-certificates \
    gnupg-agent \
    software-properties-common \
    python3-pip \
    graphviz \
    jq \
    vim \
    lsb-release 2>&1


RUN curl -fsSL https://deb.nodesource.com/setup_15.x | bash - && \
    apt-get install -y nodejs




#
# Create a non-root user to use if preferred - see https://aka.ms/vscode-remote/containers/non-root-user.
#
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME

#
# Add sudo support for the non-root user
#
RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

ENV DEBIAN_FRONTEND=dialog
