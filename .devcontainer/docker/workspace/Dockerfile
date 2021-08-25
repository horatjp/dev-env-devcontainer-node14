FROM debian:buster

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

ENV PKG="bash-completion curl dnsutils git imagemagick jq locales mariadb-client postgresql-client rsync tree unzip vim wget zip"
ENV GUI_PKG="libgtk2.0-0 libgtk-3-0 libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 libxtst6 xauth xvfb libgbm-dev fonts-ipafont chromium"
ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=ja_JP.UTF-8

RUN apt-get update && apt-get -y install $PKG $GUI_PKG \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/library-scripts \
    #
    #
    && echo "ja_JP.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    #
    # nodejs install
    && curl -sL https://deb.nodesource.com/setup_14.x | bash - \
    && apt-get install -y nodejs \
    #
    #
    && groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
