# Run IntelliJ in a container
# Inspired by jess/chrome
# OSX SPECIAL:
# ip=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}')
# xhost + $ip

# ALL ELSE (OSX invocation):
# docker run -it --net host --cpuset-cpus 0 --memory 1024mb -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=192.168.0.5:0 --name intellij e603774dc600
#
# Directories:
# Project /root/IdeaProjects
# Plugins
# 

# Base docker image
FROM ubuntu:trusty
MAINTAINER ilkka turunen <iturunen@sonatype.com>

ARG DEBIAN_FRONTEND=noninteractive
ENV _JAVA_OPTIONS="-Dawt.useSystemAAFontSettings=lcd \
                      -Dsun.java2d.xrender=true"

ENV GNOME_DESKTOP_SESSION_ID=this-is-deprecated

#Apparently this is missing because of things
RUN apt-get update && apt-get install -f -y \
	software-properties-common \
	libxtst6 \
	libfreetype6 \
	apt-transport-https \
	ca-certificates \
	curl \
	gnupg \
	hicolor-icon-theme \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	libpulse0 \
	libv4l-0 \
	libxrender1 \
	libxi-dev \
	psmisc \
	perl-base \
	perl-modules \
--no-install-recommends
RUN apt-get update && apt-get install -f -y \
git

#Accept oracle license

#RUN fuser -k /var/cache/debconf/config.dat


RUN add-apt-repository ppa:webupd8team/java && \ 
apt-get update && \
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
apt-get install -y -f oracle-java8-installer && \
update-java-alternatives -s java-8-oracle && \

wget -O /tmp/intellij.tar.gz https://download.jetbrains.com/idea/ideaIC-2016.3.2-no-jdk.tar.gz && \
tar xfz /tmp/intellij.tar.gz
# cd idea-IC-123.169/bin &&
# ./idea.sh 

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && apt-get autoremove -y

#COPY local.conf /etc/fonts/local.conf

#Dl plugin

ADD https://download.sonatype.com/iq/idea/nexus-iq-idea-plugin-1.0.2-02.zip /root/nexus-iq-plugin.zip

RUN echo -Dawt.useSystemAAFontSettings=on >> /idea-IC-163.10154.41/bin/idea64.vmoptions  && echo -Dswing.aatext=true >> /idea-IC-163.10154.41/bin/idea64.vmoptions 

# Autorun chrome
ENTRYPOINT [ "/idea-IC-163.10154.41/bin/idea.sh" ]
