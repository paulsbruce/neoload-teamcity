FROM neotys/neoload-controller

# https://github.com/JetBrains/teamcity-docker-minimal-agent
USER root
WORKDIR /opt

#RUN apk add --no-cache openjdk8-jre # && ls -latr /usr/lib/jvm/java-1.8-openjdk
#ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk/jre

ENV JAVA_HOME=/home/neoload/neoload/jre

RUN mkdir -p /opt/teamcity
ADD buildAgent.zip /opt/teamcity/

RUN unzip -qq /opt/teamcity/buildAgent.zip -d /opt/teamcity

RUN rm -r /opt/teamcity/buildAgent/conf
RUN chmod +x /opt/teamcity/buildAgent/bin/agent.sh

RUN apk add --no-cache git

ENTRYPOINT ["/bin/sh", "/opt/teamcity/buildAgent/bin/agent.sh", "run"]
