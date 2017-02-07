FROM jenkins:2.32.2

USER root

RUN apt-get update && apt-get install -y --fix-missing \
	sudo \
	docker.io \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
RUN usermod -a -G 0 jenkins

USER jenkins

#COPY plugins.txt /usr/share/jenkins/ref/
#COPY custom.groovy /usr/share/jenkins/ref/init.groovy.d/custom.groovy
#RUN /usr/local/bin/plugins.sh /usr/share/jenkins/ref/plugins.txt
