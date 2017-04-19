FROM debian:jessie-slim
MAINTAINER Kevin Minehart <kmineh0151@gmail.com>

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list

RUN apt-get update -yqqqq
RUN apt-get install -yqqqq curl golang-1.7 npm 
RUN apt-get autoremove -y
RUN apt-get clean -y

RUN curl -sL https://github.com/kminehart/jules/releases/download/v0.2.0/jules > /bin/jules
RUN curl -sL https://kubernetes-helm.storage.googleapis.com/helm-v2.3.0-linux-amd64.tar.gz | tar -xz linux-amd64/helm
RUN curl -sL https://storage.googleapis.com/kubernetes-release/release/v1.6.1/bin/linux/amd64/kubectl > /bin/kubectl
RUN mv linux-amd64/helm /bin/helm

RUN chmod +x /bin/jules
RUN chmod +x /bin/helm
RUN chmod +x /bin/kubectl

