FROM jboss/base-jdk:8

ENV MAVEN_OPTS -Xmx768m -XX:+UseConcMarkSweepGC -XX:MaxPermSize=128m -XX:+CMSClassUnloadingEnabled
ENV MAVEN_VERSION 3.3.9
ENV M2_HOME /opt/jboss/tools/maven

ENV PATH $JAVA_HOME/bin:$M2_HOME/bin:$PATH

USER root 

RUN yum -y install git \
    &&     yum clean all -y

USER jboss

# Switch to the working dir /opt/jboss
WORKDIR /opt/jboss

# Create directory tools for Maven download
RUN mkdir tools && cd tools

# Create /opt/jboss/tools/maven, download and extract Maven
RUN mkdir -p $M2_HOME && cd $M2_HOME && curl http://mirror.nbtelecom.com.br/apache/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar zx --strip 1 -C $M2_HOME

RUN cd $HOME \ 
    && mkdir -p cd $HOME/aerogear-backend-cookbook/Shoot \
    && cd $HOME/aerogear-backend-cookbook/Shoot \

WORKDIR $HOME/aerogear-backend-cookbook/Shoot

COPY . ./
USER root

RUN chown -R jboss ./*

USER jboss

EXPOSE 8080
EXPOSE 9990
EXPOSE 8443

CMD ["mvn", "wildfly-swarm:run"]

