# Run IntelliJ in a container
# Inspired by jess/chrome
# OSX SPECIAL:
# ip=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}')
# xhost + $ip

# ALL ELSE (OSX invocation):
# docker run -it --net host --cpuset-cpus 0 --memory 1024mb -v /tmp/.X11-unix:/tmp/.X11-unix -v DIRTOROOT:/root -e DISPLAY=$ip:0 --name intellij e603774dc600
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
RUN apt-get update && \
apt-get install -f -y \
	software-properties-common \ 
--no-install-recommends && \
add-apt-repository ppa:webupd8team/java && \  
apt-get update && \
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
apt-get install -f -y \
	software-properties-common \
	libxtst6 \
	libfreetype6 \
	apt-transport-https \
	ca-certificates \
	gnupg \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	libpulse0 \
	libv4l-0 \
	libxrender1 \
	libxi-dev \
	libsecret-1-0 \
	libgtk2.0-bin \ 
	libXtst6 \
	libxslt1.1 \ 
	libswt-gtk-3-java \
	gnome-keyring \
	git \
	oracle-java8-installer \
--no-install-recommends && \
update-java-alternatives -s java-8-oracle && \
apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && apt-get autoremove --purge -y


# Download intellij
#ADD  https://download.jetbrains.com/idea/ideaIC-2016.3.2-no-jdk.tar.gz /tmp/intellij.tar.gz

ADD ideaIC-2016.3.2.tar.gz /
 
#Clean up

#Dl plugin
ADD root.tar.gz /root/

# Antialiasing baby
RUN echo -Dawt.useSystemAAFontSettings=on >> /idea-IC-163.10154.41/bin/idea64.vmoptions  && echo -Dswing.aatext=true >> /idea-IC-163.10154.41/bin/idea64.vmoptions 

# Autorun intellij
ENTRYPOINT [ "/idea-IC-163.10154.41/bin/idea.sh" ]
