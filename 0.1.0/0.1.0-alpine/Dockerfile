FROM alpine:3.5
MAINTAINER Kevin Minehart <kmineh0151@gmail.com>

RUN apk add --update curl && \
    rm -rf /var/cache/apk/*

# Install Go
RUN curl -sL https://storage.googleapis.com/golang/go1.8.1.linux-amd64.tar.gz | tar zx -C /usr/local
RUN chmod +x /usr/local/go/bin/go

ENV PATH /usr/local/go/bin:$PATH
ENV GOPATH /cache/go

RUN mkdir /cache

# Install some things people will probably use
RUN curl -sL https://github.com/kminehart/jules/releases/download/0.1.0/jules > /bin/jules

RUN chmod +x /bin/jules
