FROM fedora:29
FROM ubuntu:15.04

MAINTAINER Rakesh Ummadisetty
LABEL description Robot Framework in Docker version 1.

# Setup volumes for input and output
VOLUME /opt/robotframework/reports
VOLUME /opt/robotframework/tests

# Set number of threads for parallel execution
# By default, no parallelisation
ENV ROBOT_THREADS 1

# Dependency versions
ENV PYTHON_PIP_VERSION 18.0*
ENV REQUESTS_VERSION 2.20.0
ENV ROBOT_FRAMEWORK_VERSION 3.0.4
ENV ROBOT_FRAMEWORK_REQUESTS_VERSION 0.5.0

#ENV PYTHONPATH /lib/python2.7/site-packages

# Install system dependencies
RUN dnf upgrade -y \
  && dnf install -y \
    python2-pip-$PYTHON_PIP_VERSION \
  && dnf clean all

# Install Robot Framework and Selenium Library
RUN pip2 install \
  robotframework==$ROBOT_FRAMEWORK_VERSION \
  requests==$REQUESTS_VERSION \
  robotframework-requests==$ROBOT_FRAMEWORK_REQUESTS_VERSION \
  robotframework-appiumlibrary \
  six

# Install Java 
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get update && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java7-installer && \
    apt-get clean
    
# Update system path
ENV PATH=~/opt/robotframework/bin:~/opt/robotframework/drivers:$PATH


#RUN robot \
#        --outputDir ~/Desktop/opt/robotframework/reports \
#        ${ROBOT_OPTIONS} \
#        ~/Desktop/opt/robotframework/tests
