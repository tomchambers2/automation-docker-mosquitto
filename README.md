docker-mosquitto
================

Docker image for mosquitto on a raspberry pi. Tested using hypriot OS

## Run

    docker run -tip 1883:1883 -p 9001:9001 toke/mosquitto

Exposes Port 1883 (MQTT) 9001 (Websocket MQTT)

Alternatively you can use volumes to make the changes
persistent and change the configuration.

    mkdir -p /srv/mqtt/config/
    mkdir -p /srv/mqtt/data/
    mkdir -p /srv/mqtt/log/
    # place your mosquitto.conf in /srv/mqtt/config/
    # NOTE: You have to change the permissions of the directories
    # to allow the user to read/write to data and log and read from
    # config directory
    # For TESTING purposes you can use chmod -R 777 /srv/mqtt/*
    # Better use "-u" with a valid user id on your docker host

    docker run -ti -p 1883:1883 -p 9001:9001 \
    -v /srv/mqtt/config:/mqtt/config:ro \
    -v /srv/mqtt/log:/mqtt/log \
    -v /srv/mqtt/data/:/mqtt/data/ \
    --name mqtt toke/mosquitto


Volumes: /mqtt/config, /mqtt/data and /mqtt/log


## Build

    git clone https://github.com/toke/docker-mosquitto.git
    cd docker-mosquitto
    docker build .
