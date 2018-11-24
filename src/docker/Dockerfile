FROM fedora:29

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
  
# Update system path
ENV PATH=~/opt/robotframework/bin:~/opt/robotframework/drivers:$PATH

FROM alpine:3.4

# A few problems with compiling Java from source:
#  1. Oracle.  Licensing prevents us from redistributing the official JDK.
#  2. Compiling OpenJDK also requires the JDK to be installed, and it gets
#       really hairy.

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

# add a simple script that can auto-detect the appropriate JAVA_HOME value
# based on whether the JDK or only the JRE is installed
RUN { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

ENV JAVA_VERSION 8u92
ENV JAVA_ALPINE_VERSION 8.92.14-r1

RUN set -x \
	&& apk add --no-cache \
		openjdk8="$JAVA_ALPINE_VERSION" \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ]

# Define default command.
CMD ["bash"]
#RUN robot \
#        --outputDir ~/Desktop/opt/robotframework/reports \
#        ${ROBOT_OPTIONS} \
#        ~/Desktop/opt/robotframework/tests
