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
FROM jswank:iq-server
MAINTAINER ilkka turunen <iturunen@sonatype.com>

ARG DEBIAN_FRONTEND=noninteractive
