FROM debian:buster

MAINTAINER keopx <keopx@keopx.net>

# System environments
ENV DEBIAN_FRONTEND="noninteractive" \
    LOCALE="es_ES.UTF-8" \
    GOTPL_VER="0.1.5" \
    DEFAULT_ROOT="/var/www/html" \
    UID="1000" \
    GID="1000" \
    UNAME="keopx"
#==============================================================================
# OS Setup
#==============================================================================

# Set repositories
RUN \
  echo "deb http://ftp.de.debian.org/debian/ buster main non-free contrib" > /etc/apt/sources.list && \
  echo "deb-src http://ftp.de.debian.org/debian/ buster main non-free contrib" >> /etc/apt/sources.list && \
  echo "deb http://security.debian.org/ buster/updates main contrib non-free" >> /etc/apt/sources.list && \
  echo "deb-src http://security.debian.org/ buster/updates main contrib non-free" >> /etc/apt/sources.list && \
  # Update repositories cache and distribution
  apt-get -qq update && apt-get -qqy upgrade && \
  apt-get -yqq install \
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
  nano \
  sudo && \ 
# RUN apt-get install curl-dev ruby-dev build-base sudo ruby ruby-io-console ruby-rdoc ruby-irb libffi-dev python git
  curl -sL https://deb.nodesource.com/setup_12.x | bash - ; \
  apt-get install -y nodejs && \
# Cleanup some things.
  apt-get -q autoclean && \
  rm -rf /var/lib/apt/lists/* && \ 
#==============================================================================
# Node
#==============================================================================
# Node modules
  npm install --global gulp && \
  npm install -g graceful-fs && \
  npm install -g gulp && \
  npm install --global yarn && \
  npm install --global webpack && \
#==============================================================================
# LOCAL TO THIS PROJECT
#==============================================================================
# Ruby
  gem install bundler && \
  gem install hologram && \
  gem install jekyll bundler && \
# add local user
  groupadd -g $UID $GID ; \
  useradd -m -u $UID -g $GID -s /bin/bash $UNAME ; \
  usermod -aG sudo $UNAME; \
  echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers; \
  echo ". /usr/share/bash-completion/bash_completion" >> /home/$UNAME/.bashrc && echo "alias ll='ls -lahs'" >> /home/$UNAME/.bashrc ; \
  echo ". /usr/share/bash-completion/bash_completion" >> ~/.bashrc && echo "alias ll='ls -lahs'" >> ~/.bashrc

USER keopx

EXPOSE 80 3000 4000 9000

CMD ["tail","-f","/dev/null"]
