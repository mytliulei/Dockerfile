FROM ioft/i386-ubuntu:14.04
MAINTAINER Liu Lei <mytliulei@gmail.com>

RUN rm -rf /var/lib/apt/lists/*
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
COPY ./sources.list /etc/apt/sources.list
RUN linux32 apt-get update \
    && linux32 apt-get install -y gcc \
    python2.7 \
    python2.7-dev \
    python-pip
RUN mkdir -p /tmp/tcl
COPY ./tcl8.5.9-src.tar.gz /tmp/tcl/
COPY ./tcllib-tcllib_1_18.tar.gz /tmp/tcl
WORKDIR /tmp/tcl
RUN tar -zxvf tcl8.5.9-src.tar.gz
RUN tar -zxvf tcllib-tcllib_1_18.tar.gz
WORKDIR tcl8.5.9/unix
RUN linux32 ./configure --disable-shared
RUN linux32 make
RUN linux32 make install
WORKDIR /tmp/tcl/tcllib-tcllib_1_18
RUN linux32 tclsh8.5 installer.tcl -no-wait
WORKDIR /home/
ENV AV_PROXY_DOCKER=1

RUN mkdir -p /tmp/java
COPY ./jre-6u41-linux-i586.bin /tmp/java/
WORKDIR /tmp/java
RUN chmod 755 jre-6u41-linux-i586.bin
RUN ./jre-6u41-linux-i586.bin
RUN cp -r /tmp/java /usr/lib/java

ENV JAVA_HOME="/usr/lib/java/jre1.6.0_41"
#  CLASSPATH="/usr/lib/java/jre1.6.0_41/lib" \
#  PATH="/usr/lib/java/jre1.6.0_41/bin"
RUN update-alternatives --install /usr/bin/java java /usr/lib/java/jre1.6.0_41/bin/java 300

WORKDIR /home/
ENTRYPOINT ["linux32"]

