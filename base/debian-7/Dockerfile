#++++++++++++++++++++++++++++++++++++++
# Debian 7 Base Docker container
#++++++++++++++++++++++++++++++++++++++

FROM webdevops/bootstrap:debian-7
MAINTAINER info@webdevops.io

ENV APPLICATION_USER  application
ENV APPLICATION_GROUP application
ENV APPLICATION_UID   1000
ENV APPLICATION_GID   1000
ENV DOCKER_CONF_HOME  /opt/docker/

# Install services
RUN sed -ri 's/(deb.*\/debian wheezy main)/\1 contrib non-free /' -- /etc/apt/sources.list \
    && /usr/local/bin/apt-install \
        supervisor \
        syslog-ng \
        syslog-ng-core \
        logrotate \
        openssh-server \
        mysql-client \
        cron \
        dnsmasq \
        postfix

# Install common tools
RUN /usr/local/bin/apt-install \
        lsb-release \
        sudo \
        zip \
        unzip \
        bzip2 \
        wget \
        curl \
        net-tools \
        moreutils \
        dnsutils \
        openssh-client \
        rsync \
        git \
        nano \
        vim

# Deploy scripts/configurations
COPY conf/ /opt/docker/
RUN bash /opt/docker/bin/control.sh provision.role webdevops-base \
    && bash /opt/docker/bin/control.sh provision.role.finish webdevops-cleanup \
    && bash /opt/docker/bin/bootstrap.sh

ENTRYPOINT ["/opt/docker/bin/entrypoint.sh"]
CMD ["noop"]
