#################################################################
# Dockerfile to build Zimbra Collaboration 8.8.7 container images
# Based on Ubuntu 16.04
# Created by Jorge de la Cruz
#################################################################
FROM ubuntu:16.04
MAINTAINER Jorge de la Cruz <jorgedlcruz@gmail.com>

RUN echo "resolvconf resolvconf/linkify-resolvconf boolean false" | debconf-set-selections

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install \
  wget \
  dialog \
  openssh-client \
  software-properties-common \
  dnsmasq \
  dnsutils \
  net-tools \
  sudo \
  rsyslog \
  unzip


RUN set -ex && \
  mkdir -p /opt/zimbra-install && \
  echo "Downloading Zimbra Collaboration 8.8.7" && \
  wget -O /opt/zimbra-install/zimbra-zcs-8.8.7.tar.gz https://files.zimbra.com/downloads/8.8.7_GA/zcs-8.8.7_GA_1964.UBUNTU16_64.20180223145016.tgz && \
  echo "Extracting files from the archive" && \
  tar xzvf /opt/zimbra-install/zimbra-zcs-8.8.7.tar.gz -C /opt/zimbra-install/ && \
  echo "Update package cache" && \
  apt update

#VOLUME ["/opt/zimbra"]

EXPOSE 22 25 465 587 110 143 993 995 80 443 8080 8443 7071

COPY opt /opt/

COPY etc /etc/

CMD ["/bin/bash", "/opt/start.sh", "-d"]
