FROM ubuntu:focal

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

# Default values for final container username and UID/GID
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000

# Configure apt and install packages (2>&1 combines stderr and stdout)
RUN apt-get update \
    && apt-get -y install --no-install-recommends sudo apt-utils dialog 2>&1 
    
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
    lsof \
    vim \
    lsb-release 2>&1

#
# install the node 15 nodesource apt repo and install nodejs 
#
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

#
# This doesn't actually expose the port, it's like an interfce telling the client that the ports will be required
#
EXPOSE 19000
EXPOSE 19001
EXPOSE 19002

#
# Switch to the non root user
#
USER $USERNAME

#
# Add NPM Global to the path
#
ENV PATH="/home/$USERNAME/.npm-global:/home/$USERNAME/.npm-global/bin:${PATH}"

#
# Install yarn package manage
#
RUN sudo npm install --global yarn

# install global yarn package
RUN sudo yarn global add expo-cli


ENV DEBIAN_FRONTEND=dialog
