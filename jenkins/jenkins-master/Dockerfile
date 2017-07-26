#FROM jenkins:1.651.3
FROM jenkins:2.7.4

USER root

RUN apt-get update && apt-get install -y vim locales 

ENV TZ "Asia/Shanghai"
RUN echo "Asia/Shanghai" | tee /etc/timezone \
  && dpkg-reconfigure --frontend noninteractive tzdata

RUN locale-gen C.UTF-8 &&\
  DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales
ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8  
ENV LC_ALL C.UTF-8

USER ${user}
ENV JAVA_OPTS="-Dhudson.model.DirectoryBrowserSupport.CSP= -Dfile.encoding=UTF-8"

RUN rm -rf /var/lib/apt/lists/*
