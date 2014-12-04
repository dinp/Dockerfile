FROM centos:centos6

RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN yum -y install wget tar unzip gcc zlib zlib-devel openssl openssl-devel build-essential ca-certificates git mercurial bzr unzip
RUN mkdir /goroot && curl http://golangtc.com/static/go/go1.3.1.linux-amd64.tar.gz | tar xvzf - -C /goroot --strip-components=1
RUN mkdir /gopath /opt/app /opt/logs

ADD . /opt/
WORKDIR /opt

RUN tar zxvf scribed.tar.gz \
    && chown -R root:root scribed \
    && rm -f scribed.tar.gz

RUN curl -SL 'https://bootstrap.pypa.io/get-pip.py' | python
RUN pip install supervisor \
    && echo_supervisord_conf > /etc/supervisord.conf \
    && echo "[include]" >> /etc/supervisord.conf \
    && echo "files = /etc/supervisord.d/*.conf" >> /etc/supervisord.conf \
    && mkdir -p /etc/supervisord.d \
    && cp go.conf scribed.conf /etc/supervisord.d/ \
    && rm -f go.conf scribed.conf Dockerfile

ENV GOROOT /goroot
ENV GOPATH /gopath
ENV APP /opt/app
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin:$APP
