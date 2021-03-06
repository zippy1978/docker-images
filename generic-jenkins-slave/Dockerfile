# This Dockerfile is based on evarga/jenkins-slave
# This Dockerfile is used to build an image containing basic stuff to be used as a Jenkins slave build node.
FROM ubuntu:trusty
MAINTAINER Gilles Grousset <gi.grousset@gmail.com>

# Sets language to UTF8 : this works in pretty much all cases
ENV LANG en_US.UTF-8
RUN locale-gen $LANG

# Make sure the package repository is up to date.
RUN apt-get update
RUN apt-get -y upgrade

# Install a basic SSH server
RUN apt-get install -y openssh-server software-properties-common
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd

# Setup the openjdk 8 repo
RUN add-apt-repository ppa:openjdk-r/ppa

# Install JDK 7 (latest edition)
RUN apt-get update && apt-get install -y openjdk-8-jdk

# Setup JAVA_HOME, this is useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

# Install Git
RUN apt-get install -y git

# Add user jenkins to the image
RUN adduser --quiet jenkins
# Set password for the jenkins user (you may want to alter this).
RUN echo "jenkins:jenkins" | chpasswd

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
