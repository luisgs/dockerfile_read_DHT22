# Dockerfile for read DHT values script

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://github.com/luisgs/read_expose_dht_sensors.git)

Dockerfile that creates a docker image that will run this script:
- https://github.com/luisgs/read_expose_dht_sensors.git

Dockerizing this script allows us to spin several instances without maintainance.

## Docker

Dockerfile will expose data via port 8000 by default, but it can be changed within the
Dockerfile if necessary or during executition of the docker itself (compose). When ready, simply use the Dockerfile to
build the image.

```sh
sudo docker build -t dockerfile_dht22 .
```

Example of running this docker image for a DHT22 sensor connected at PIN 17th and with 30 seconds read interval.
```sh
sudo docker run --privileged -v /sys:/sys -e pin=17 -e sleep=30 -dp 0.0.0.0:8040:8000 dockerfile_dht22
```

Docker compose can look like this:
```yaml
version: '3'
services:
  dht22:
    image: paneraccoon/dht22_docker:latest
    container_name: DHT22_external
    privileged: true
    restart: unless-stopped
    volumes:
      - /sys:/sys 
    environment:
      - 'pin=17'
      - 'sleep=30'
    ports:
     - 8010:8000
  ```
