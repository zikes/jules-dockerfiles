FROM golang:1.8.1-stretch
MAINTAINER Kevin Minehart <kmineh0151@gmail.com>

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list

RUN apt-get update -yqqqq
# RUN apt-get install -yqqqq curl
RUN apt-get install -yqqqq curl autoconf automake libtool pkg-config
RUN apt-get autoremove -y
RUN apt-get clean -y

# Install some things people will probably use
RUN curl -sL https://github.com/kminehart/jules/releases/download/v0.2.4/jules > /bin/jules                                                                                           

RUN git clone https://github.com/openvenues/libpostal
RUN cd libpostal && \
  bash bootstrap.sh && \
  bash configure --datadir="/data" && \
  make && \
  make install

# On Linux it's probably a good idea to run
RUN ldconfig

RUN chmod +x /bin/jules

RUN go get github.com/tools/godep

WORKDIR $GOPATH
