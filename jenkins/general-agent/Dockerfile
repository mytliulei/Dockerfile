FROM evarga/jenkins-slave:latest
MAINTAINER Liu Lei <mytliulei@gmail.com>

RUN apt-get update

ENV TZ "Asia/Shanghai"
RUN echo "Asia/Shanghai" | tee /etc/timezone \
  && dpkg-reconfigure --frontend noninteractive tzdata

RUN apt-get update && \
    apt-get install -y -f vim curl wget


RUN usermod -s /bin/bash jenkins
ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8
ENV LC_ALL C.UTF-8
RUN sed -i "1iexport LANG=C.UTF-8" /home/jenkins/.bashrc
RUN sed -i "2iexport LANGUAGE=en_US:en" /home/jenkins/.bashrc
RUN sed -i "3iexport LC_ALL=C.UTF-8"  /home/jenkins/.bashrc
