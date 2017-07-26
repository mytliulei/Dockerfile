FROM evarga/jenkins-slave:latest
MAINTAINER Liu Lei <mytliulei@gmail.com>

#COPY sources.list /etc/apt/sources.list
RUN apt-get update

#ENV TZ "RPC"
ENV TZ "Asia/Shanghai"
RUN echo "Asia/Shanghai" | tee /etc/timezone \
  && dpkg-reconfigure --frontend noninteractive tzdata

RUN apt-get update && \
    apt-get install -y -f gcc vim curl wget \
    python2.7 python-pip python2.7-dev libssl-dev libffi-dev \
    libpcap-dev tcpdump tshark
RUN pip install robotframework
RUN pip install pyparsing
RUN pip install appdirs
RUN pip install six==1.6.0
RUN pip install paramiko
RUN pip install pyte==0.4.8
RUN pip install pcapy
#RUN pip install dnet
RUN pip install redis
RUN pip install ecdsa
RUN pip install pyreadline
RUN pip install pygal
#RUN pip install pcap-fix
RUN pip install scapy==2.2.0-dev
RUN pip install robotframework-sshlibrary
RUN pip install docker-py


RUN usermod -s /bin/bash jenkins
ENV DEBIAN_FRONTEND noninteractive
#RUN locale-gen C.UTF-8
#RUN dpkg-reconfigure --frontend noninteractive locales
ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8
ENV LC_ALL C.UTF-8
RUN sed -i "1iexport LANG=C.UTF-8" /home/jenkins/.bashrc
RUN sed -i "2iexport LANGUAGE=en_US:en" /home/jenkins/.bashrc
RUN sed -i "3iexport LC_ALL=C.UTF-8"  /home/jenkins/.bashrc



ENV CHROME_DRIVER_VERSION 2.29
ENV LANG C.UTF-8
ENV DISPLAY :99

RUN  echo "deb http://archive.ubuntu.com/ubuntu trusty main universe\n" > /etc/apt/sources.list \
  && echo "deb http://archive.ubuntu.com/ubuntu trusty-updates main universe\n" >> /etc/apt/sources.list

RUN apt-get update -qqy \
  && apt-get -qqy install build-essential wget unzip curl xvfb xz-utils zlib1g-dev libssl-dev


RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
  && apt-get update -qqy \
  && apt-get -qqy install google-chrome-stable \
  && rm /etc/apt/sources.list.d/google-chrome.list \
  && rm -rf /var/lib/apt/lists/*

RUN wget --no-verbose -O /tmp/chromedriver_linux64.zip http://chromedriver.storage.googleapis.com/$CHROME_DRIVER_VERSION/chromedriver_linux64.zip \
  && rm -rf /opt/selenium/chromedriver \
  && unzip /tmp/chromedriver_linux64.zip -d /opt/selenium \
  && rm /tmp/chromedriver_linux64.zip \
  && mv /opt/selenium/chromedriver /opt/selenium/chromedriver-$CHROME_DRIVER_VERSION \
  && chmod 755 /opt/selenium/chromedriver-$CHROME_DRIVER_VERSION \
  && ln -fs /opt/selenium/chromedriver-$CHROME_DRIVER_VERSION /usr/bin/chromedriver

RUN DEBIAN_FRONTEND=noninteractive apt-get update -qqy \
 && pip install --upgrade pip \
 && pip install -I unittest-xml-reporting==1.12.0 \
 && pip install robotframework \
 && pip install -U robotframework-selenium2library \
 && pip install -U selenium


#==================
# Xvfb + init scripts
#==================
ADD libs/xvfb_init /etc/init.d/xvfb
RUN chmod a+x /etc/init.d/xvfb

ADD libs/xvfb-daemon-run /usr/bin/xvfb-daemon-run
RUN chmod a+x /usr/bin/xvfb-daemon-run


#============================
# Clean up
#============================
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ~/.config/google-chrome

RUN apt-get update -qqy \
 && apt-get -qqy install language-pack-zh-hans \
 && apt-get install -y --force-yes --no-install-recommends fonts-wqy-microhei fonts-wqy-zenhei

COPY local /var/lib/locales/supported.d/

RUN locale-gen zh_CN.UTF-8 \
 && DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales
RUN locale-gen zh_CN.UTF-8

ENV LANG zh_CN.UTF-8
ENV LANGUAGE zh_CN:zh
ENV LC_ALL zh_CN.UTF-8


RUN sed -i "4iexport LANG=zh_CN.UTF-8" /home/jenkins/.bashrc
RUN sed -i "5iexport LANGUAGE=zh_CN:zh" /home/jenkins/.bashrc
RUN sed -i "6iexport LC_ALL=zh_CN.UTF-8" /home/jenkins/.bashrc



