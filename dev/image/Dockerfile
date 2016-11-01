FROM debian:8.6

# Arguments that must be supplied with --build-arg
ARG USER_NAME_ON_HOST
ARG USER_ID_ON_HOST
RUN if [ -z "$USER_NAME_ON_HOST" ]; then echo 'USER_NAME_ON_HOST must be supplied'; exit 1; fi
RUN if [ -z "$USER_ID_ON_HOST" ]; then echo 'USER_ID_ON_HOST must be supplied'; exit 1; fi

# Install pre-requisites
RUN \
  apt-get update && \
  apt-get install -y apt-utils curl git sudo tmux vim wget

# Create user
RUN \
  adduser --uid $USER_ID_ON_HOST --disabled-password --gecos "" $USER_NAME_ON_HOST && \
  echo "$USER_NAME_ON_HOST ALL=NOPASSWD: ALL" | (EDITOR="tee -a" visudo)

# Install Node
RUN \
  curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
  apt-get install -y nodejs && \
  node --version

# Install Yarn
RUN \
  npm install -g yarn && \
  yarn --version

# Add files
ADD files /
