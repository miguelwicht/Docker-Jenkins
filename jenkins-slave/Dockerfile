FROM ubuntu:16.04

run apt-get update && apt-get install -y \
    openssh-server \
    openjdk-8-jre-headless \
    git \
    curl \
    zip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm -f /var/cache/apt/*.bin \
    && sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd \
    && mkdir -p /var/run/sshd

# Set user jenkins to the image
RUN useradd -m -d /home/jenkins -s /bin/bash jenkins &&\
    echo "jenkins:jenkins" | chpasswd

RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    && apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D \
    && echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" >> /etc/apt/sources.list.d/docker.list \
    && apt-get update \
    && apt-get purge lxc-docker \
    && apt-cache policy docker-engine \
    && apt-get update \
    && apt-get install -y docker-engine \
    && apt-get -q clean -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm -f /var/cache/apt/*.bin

RUN apt-get update && apt-get install -y \
    sudo \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm -f /var/cache/apt/*.bin

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
RUN usermod -aG docker jenkins
RUN usermod -aG root jenkins
RUN usermod -aG 50 jenkins

#RUN echo "jenkins    ALL=(ALL)    ALL" >> etc/sudoers


# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]
