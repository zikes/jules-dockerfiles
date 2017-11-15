FROM golang:1.9.2-stretch
MAINTAINER Kevin Minehart <kmineh0151@gmail.com>

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list

RUN apt-get update -yqqqq
RUN apt-get install -yqqqq curl autoconf automake libtool pkg-config make g++ unzip

# Install docker
# # Dependencies
RUN apt-get install -yqqqq \
     apt-transport-https \
     ca-certificates \
     gnupg2 \
     software-properties-common
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add -

RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable"
RUN apt-get update -yq
RUN apt-get install docker-ce -yq
RUN apt-get autoremove -yq
RUN apt-get clean -yq

# Install some things people will probably use
RUN curl -sL https://github.com/kminehart/jules/releases/download/v0.2.4/jules > /bin/jules                                                                                           

RUN git clone https://github.com/openvenues/libpostal

RUN cd libpostal && bash bootstrap.sh
RUN cd libpostal && bash configure --datadir="/data"
RUN cd libpostal && make
RUN cd libpostal && make install

# On Linux it's probably a good idea to run
RUN ldconfig

RUN chmod +x /bin/jules

RUN go get github.com/tools/godep
RUN go get golang.org/x/tools/cmd/goimports
RUN go get github.com/golang/lint/golint
RUN go get -u -d github.com/zikes/migrate/cli github.com/cockroachdb/cockroach-go/crdb
RUN go get -u google.golang.org/grpc
RUN go get -u github.com/golang/protobuf/proto
RUN go get -u github.com/golang/protobuf/protoc-gen-go

RUN wget https://github.com/google/protobuf/archive/v3.5.0.tar.gz && \
  tar -xvf v3.5.0.tar.gz && cd protobuf-3.5.0 && \
  ./autogen.sh && ./configure && make && make install && ldconfig
# RUN wget https://github.com/google/protobuf/releases/download/v3.5.0/protoc-3.5.0-linux-x86_64.zip && \
#   unzip protoc-3.5.0-linux-x86_64.zip && \
#   mv bin/protoc /bin && \
#   mv include/* /usr/include && \
#   chmod +x /bin/protoc && \
#   ls /usr/include/google/protobuf

WORKDIR $GOPATH
