FROM php:5.6
MAINTAINER Dealerdirect

ENV COMPOSER_HOME /root/.composer
ENV PATH $PATH:$COMPOSER_HOME/vendor/bin
ENV DEBIAN_FRONTEND noninteractive
ENV BUILD_DEPS "python-pip build-essential python-dev libssl-dev libffi-dev"
ENV INSTALL_APT "ruby sudo python python-setuptools nodejs git unzip libxml2-utils ssh"
ENV INSTALL_PIP "yamllint flake8"
ENV INSTALL_GEM "rubocop"
ENV INSTALL_NPM "jsonlint"

ADD php.ini /usr/local/etc/php/php.ini

RUN \
    curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get update \
    && apt-get install -y --no-install-recommends $BUILD_DEPS $INSTALL_APT \
    && gem install $INSTALL_GEM \
    && pip install $INSTALL_PIP \
    && npm install $INSTALL_NPM -g \
    && docker-php-ext-install bcmath \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && mkdir /root/.ssh \
    && touch /root/.ssh/known_hosts \
    && ssh-keyscan bitbucket.org >> /root/.ssh/known_hosts \
    && ssh-keyscan github.com >> /root/.ssh/known_hosts \
    && curl -O https://raw.githubusercontent.com/DealerDirect/php-qa-tools/master/bin/install.sh \
    && bash install.sh \
    && rm -f install.sh \
    && apt-get remove -y --purge $BUILD_DEPS \
    && apt-get -y purge \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc \
    && rm -Rf /usr/share/man
