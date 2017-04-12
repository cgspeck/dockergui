# Docker dockergui

## Description:
dockergui is a base image based of phusion's base image version 0.9.19 with ssh disabled.

This gives you a Ubuntu 16.04 LTS (Xenal) base.

This Docker image makes it possible to use any X application on a headless server through a modern web browser such as chrome with X11rdp to run its virtual X server

Xrdp is installed and the container can be accessed using any rdp client. You can access the web interface by going to port 8080 or rdp via port 3389.


## How to use this image:

### Example docker file:

```
# Builds a docker gui image
FROM hurricane/dockergui:xvnc

#########################################
##        ENVIRONMENTAL CONFIG         ##
#########################################

# Set environment variables

# User/Group Id gui app will be executed as default are 99 and 100
ENV USER_ID=99
ENV GROUP_ID=100

# Gui App Name default is "GUI_APPLICATION"
ENV APP_NAME GUI_APPLICATION

# Default resolution, change if you like
ENV WIDTH=1280
ENV HEIGHT=720

# Use baseimage-docker's init system
CMD ["/sbin/my_init"]

#########################################
##    REPOSITORIES AND DEPENDENCIES    ##
#########################################
RUN echo 'deb http://us.archive.ubuntu.com/ubuntu/ xenial main universe restricted' > /etc/apt/sources.list
RUN echo 'deb http://us.archive.ubuntu.com/ubuntu/ xenial-updates main universe restricted' >> /etc/apt/sources.list
RUN apt-get update

# Install packages needed for app

# Install packages needed for app

#########################################
##          GUI APP INSTALL            ##
#########################################

# Install steps for X app

# Copy X app start script to right location
COPY startapp.sh /startapp.sh

#########################################
##         EXPORTS AND VOLUMES         ##
#########################################

# Place whatever volumes and ports you want exposed here:

```

## Environment Variables

The dockergui image uses several optional environment variables. All the ones listed in the example above plus the following:

`TZ` - This environment variable is used to set the [TimeZone] of the container.

[TimeZone]: http://en.wikipedia.org/wiki/List_of_tz_database_time_zones

## Build from docker file (Info only, not required.):

```
git clone --depth=1 https://github.com/cgspeck/dockergui.git
cd dockergui
docker build --rm=true -t dockergui .
```
