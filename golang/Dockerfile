FROM centos:centos6

RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN yum -y install wget tar unzip gcc zlib zlib-devel openssl openssl-devel build-essential ca-certificates git mercurial bzr unzip
RUN mkdir /goroot && curl http://golangtc.com/static/go/go1.3.1.linux-amd64.tar.gz | tar xvzf - -C /goroot --strip-components=1
RUN mkdir /gopath
RUN mkdir /opt/app

ENV GOROOT /goroot
ENV GOPATH /gopath
ENV APP /opt/app
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin:$APP
