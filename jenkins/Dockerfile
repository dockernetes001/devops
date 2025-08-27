FROM jenkins/jenkins:lts

USER root

# Instalar Node.js, npm, yarn y utilidades
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get update \
    && apt-get install -y \
       nodejs git \
       npm \
       yarn \
       xvfb \
       libgtk2.0-0 \
       libgtk-3-0 \
       libnotify-dev \
       libgconf-2-4 \
       libnss3 \
       libxss1 \
       libasound2 \
       libxtst6 \
       fonts-liberation \
       libappindicator3-1 \
       libgbm1 \
       wget \
       unzip \
    && npm install -g yarn \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Volver a usuario jenkins
USER jenkins
