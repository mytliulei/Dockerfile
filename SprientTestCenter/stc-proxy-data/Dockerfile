# VERSION     0.1

FROM ioft/i386-ubuntu:14.04
MAINTAINER Liu Lei <mytliulei@gmail.com>
ARG stc_version

RUN mkdir -p /tmp/spirent
COPY ./Spirent_TestCenter_Auto_Linux_${stc_version}.tar.gz /tmp/spirent/
WORKDIR /tmp/spirent
RUN tar -zxvf Spirent_TestCenter_Auto_Linux_${stc_version}.tar.gz
RUN mkdir -p /usr/local/lib/tcl8.5/stc2.0
RUN cp -r Spirent_TestCenter_${stc_version}/Spirent_TestCenter_Application_Linux/* /usr/local/lib/tcl8.5/stc2.0/
RUN rm -rf /tmp/spirent/*
RUN rm -rf /usr/local/lib/tcl8.5/stc2.0/results_reporter/*
ENV STC_PROXY_DOCKER=1
ENTRYPOINT ["linux32"]
VOLUME ["/usr/local/lib/tcl8.5/stc2.0"]
