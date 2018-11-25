FROM fedora:29

MAINTAINER Rakesh Ummadisetty
LABEL description Robot Framework in Docker version 1.

# Setup volumes for input and output
VOLUME ~/opt/robotframework/reports
VOLUME ~/opt/robotframework/tests

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

FROM picoded/ubuntu-base
MAINTAINER Eugene Cheah <eugene@picoded.com>

# This is in accordance to : https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-get-on-ubuntu-16-04
RUN apt-get update && \
	apt-get install -y openjdk-8-jdk && \
	apt-get install -y ant && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk8-installer;
	
# Fix certificate issues, found as of 
# https://bugs.launchpad.net/ubuntu/+source/ca-certificates-java/+bug/983302
RUN apt-get update && \
	apt-get install -y ca-certificates-java && \
	apt-get clean && \
	update-ca-certificates -f && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk8-installer;

# Setup JAVA_HOME, this is useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

RUN cp ~Documents/Kitematic/robotframework/opt/robotframework/tests ~/opt/robotframework/tests
#FROM qxf2rohand/qxf2_pom_essentials
#MAINTAINER Qxf2 Services
 
#Install git
#RUN apt-get update \
#    && apt-get install -y git
 
#Change directory and clone Qxf2 Public POM repo
#RUN cd ~/opt/robotframework/tests \
#    && git clone https://github.com/raka2407/robotframework.git
 
#Set working directory
#WORKDIR ~/opt/robotframework/tests
    
#RUN robot \
 #       --outputDir ~Documents/Kitematic/robotframework/opt/robotframework/reports \
 #      ${ROBOT_OPTIONS} \
 #       ~Documents/Kitematic/robotframework/opt/robotframework/tests
