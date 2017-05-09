# docker-sumo

[![Join the chat at https://gitter.im/docker-sumo/Lobby](https://badges.gitter.im/docker-sumo/Lobby.svg)](https://gitter.im/docker-sumo/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[![Build Status](https://travis-ci.org/bogaotory/docker-sumo.svg?branch=master)](https://travis-ci.org/bogaotory/docker-sumo)
[![](https://images.microbadger.com/badges/version/bogaotory/sumo:0.30.0.svg)](https://microbadger.com/images/bogaotory/sumo:0.30.0)
[![](https://images.microbadger.com/badges/image/bogaotory/sumo:0.30.0.svg)](https://microbadger.com/images/bogaotory/sumo:0.30.0)

Containerised SUMO.

[SUMO (Simulation of Urban MObility)](http://sumo.dlr.de/wiki/Simulation_of_Urban_MObility_-_Wiki), an open-source traffic simulation software, is dockeried by the `Dockerfile` included in this repository. This image uses Ubuntu version 16.04 and contains version 0.30.0 of SUMO.

**`sumo`**, **`sumo-gui`** and **`TraCI`** are all accessible with this image.

See `sumo-gui` in action:

![demo sumo and sumo-gui in docker](https://github.com/bogaotory/docker-sumo/blob/master/docker-sumo-demo1.gif)

See `TraCI` in action:

![demo TraCI and sumo-gui in docker](https://github.com/bogaotory/docker-sumo/blob/master/docker-sumo-demo2.gif)


## Usage (Option 1) - Build from Ubuntu image (Recommended)

1. Change `your_username` (line 8 of `Dockerfile`) to your username (i.e. the output of `echo "$USER"`)
2. Build the image with `docker build - < Dockerfile -t docker-sumo`
3. Run the image with
```
docker run -it --rm\
    --env="DISPLAY" \
    --volume="/etc/group:/etc/group:ro" \
    --volume="/etc/passwd:/etc/passwd:ro" \
    --volume="/etc/shadow:/etc/shadow:ro" \
    --volume="/etc/sudoers.d:/etc/sudoers.d:ro" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    --user=$USER \
    docker-sumo \
    bash
```
4. Execute `sumo` or `sumo-gui` as usual.

## Usage (Option 2) - Build from bogaotory/sumo:0.30.0

1. Prepare your own `Dockerfile` with your username (i.e. the output of `echo "$USER"`):
```
FROM bogaotory/sumo:0.30.0

RUN adduser your_username --disabled-password
```
2. Build the image with `docker build - < Dockerfile -t docker-sumo`
3. Run the image with
```
docker run -it --rm\
    --env="DISPLAY" \
    --volume="/etc/group:/etc/group:ro" \
    --volume="/etc/passwd:/etc/passwd:ro" \
    --volume="/etc/shadow:/etc/shadow:ro" \
    --volume="/etc/sudoers.d:/etc/sudoers.d:ro" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    --user=$USER \
    docker-sumo \
    bash
```
4. Execute `sumo` or `sumo-gui` as usual.

## References
I referenced a couple of past attempts of dockerising SUMO:

- [https://github.com/radiganm/dockerhub](https://github.com/radiganm/dockerhub), which insists on compiling everything from source
- [https://github.com/similitude/sumo-docker](https://github.com/similitude/sumo-docker), based on Maven and emphasises on the inclusion of `TraCI4J` which is not necessarily useful for beginners of SUMO.

Neither gives a straightforward containerised SUMO solution.

The method for GUI access is borrowed from [this post](http://wiki.ros.org/docker/Tutorials/GUI).




