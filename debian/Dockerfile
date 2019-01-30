FROM debian:stretch

MAINTAINER keopx <keopx@keopx.net>

ENV DEBIAN_FRONTEND noninteractive

ARG UID=1000
ARG GID=1000
ARG UNAME=keopx

#==============================================================================
# OS Setup
#==============================================================================

# Set repositories
RUN \
  echo "deb http://ftp.de.debian.org/debian/ stretch main non-free contrib\n" > /etc/apt/sources.list && \
  echo "deb-src http://ftp.de.debian.org/debian/ stretch main non-free contrib\n" >> /etc/apt/sources.list && \
  echo "deb http://security.debian.org/ stretch/updates main contrib non-free\n" >> /etc/apt/sources.list && \
  echo "deb-src http://security.debian.org/ stretch/updates main contrib non-free" >> /etc/apt/sources.list && \
  # Update repositories cache and distribution
  apt-get -qq update && apt-get -qqy upgrade

# Update repositories cache and distribution
RUN apt-get -qq update && apt-get -qqy upgrade

RUN apt-get -yqq install \
  apt-utils \
  build-essential \
  debconf-utils \
  debconf \
  locales \
  curl \
  wget \
  unzip \
  patch \
  rsync \
  openssh-client \
  git \
  bash-completion \
  locales \
  ruby-dev \
  ruby \
  ruby-full \
  build-essential \
  sudo
 
# RUN apt-get install curl-dev ruby-dev build-base sudo ruby ruby-io-console ruby-rdoc ruby-irb libffi-dev python git

RUN curl -sL https://deb.nodesource.com/setup_11.x | bash - ; \
  apt-get install -y nodejs
#==============================================================================
# LAMP Setup
#==============================================================================

# add local user
RUN \
  groupadd -g $UID $GID ; \
  useradd -m -u $UID -g $GID -s /bin/bash $UNAME ; \
  usermod -aG sudo $UNAME; \
  echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers; \
  echo ". /usr/share/bash-completion/bash_completion" >> /home/$UNAME/.bashrc && echo "alias ll='ls -lahs'" >> /home/$UNAME/.bashrc ; \
  echo ". /usr/share/bash-completion/bash_completion" >> ~/.bashrc && echo "alias ll='ls -lahs'" >> ~/.bashrc

#==============================================================================
# Node
#==============================================================================
# Node modules
RUN npm install --global gulp 
RUN npm install -g graceful-fs && npm install -g gulp
RUN npm install --global yarn
RUN npm install --global webpack

#==============================================================================
# LOCAL TO THIS PROJECT
#==============================================================================
# Ruby
RUN gem install bundler
RUN gem install hologram
RUN gem install jekyll bundler

USER keopx

EXPOSE 80 3000 9000

CMD ["tail","-f","/dev/null"]
