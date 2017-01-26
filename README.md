# docker-gui-apps
A repo for containerised GUI apps. Heavily inspired by https://blog.jessfraz.com/post/docker-containers-on-the-desktop/  

# Initialisation
1 Read Dockerfile for running instructions

ONLY For OSX:
* Install Latest XQuartz (might affect display resolution if retina so be aware) : https://www.xquartz.org/
* Install socat
* Run Socat: 
socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
* Add your eth ip to accepted list: 
xhost + $ip

