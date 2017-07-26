FROM ioft/i386-ubuntu:14.04
MAINTAINER Liu Lei <mytliulei@gmail.com>

ARG av_version

RUN mkdir -p /tmp/av
COPY ./Layer_4_7_Auto_Linux_${av_version}.tar.gz /tmp/av
COPY ./unix32.tar.gz /tmp/av
WORKDIR /tmp/av
RUN tar -zxvf Layer_4_7_Auto_Linux_${av_version}.tar.gz
RUN tar -zxvf unix32.tar.gz
RUN mkdir -p /usr/local/lib/tcl8.5/av
RUN cp -r Layer_4_7_Auto_Linux_${av_version}/Layer_4_7_Application_Linux/* /usr/local/lib/tcl8.5/av
RUN cp -r unix32 /usr/local/lib/tcl8.5/av
RUN rm -rf /tmp/av/*
#RUN rm -rf /usr/local/lib/tcl8.5/av/
ENV STC_PROXY_DOCKER=1
ENTRYPOINT ["linux32"]
VOLUME ["/usr/local/lib/tcl8.5/av"]
