FROM ubuntu:16.04

MAINTAINER Bo Gao (bogao@dcs.warwick.ac.uk)
LABEL Description="Dockerised Simulation of Urban MObility(SUMO)"

ENV SUMO_VERSION 0.30.0
ENV SUMO_HOME /opt/sumo
ENV SUMO_USER your_username

# Install system dependencies.
RUN apt-get update && apt-get -qq install \
    wget \
    g++ \
    make \
    libxerces-c-dev \
    libfox-1.6-0 libfox-1.6-dev \
    python2.7

# Download and extract source code
RUN wget http://downloads.sourceforge.net/project/sumo/sumo/version%20$SUMO_VERSION/sumo-src-$SUMO_VERSION.tar.gz
RUN tar xzf sumo-src-$SUMO_VERSION.tar.gz && \
    mv sumo-$SUMO_VERSION $SUMO_HOME && \
    rm sumo-src-$SUMO_VERSION.tar.gz

# Configure and build from source.
RUN cd $SUMO_HOME && ./configure && make install

RUN adduser $SUMO_USER --disabled-password
# CMD sumo-gui