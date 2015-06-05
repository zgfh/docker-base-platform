FROM maven:3-jdk-7

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME

ENV TOMCAT_MAJOR 7
ENV TOMCAT_VERSION 7.0.57

#add maven
RUN apt-get -y --force-yes install   maven

#you can get at http://mirrors.cnnic.cn/apache/tomcat/tomcat-7/v7.0.57/bin/apache-tomcat-7.0.57.tar.gz
ADD apache-tomcat-7.0.57.tar.gz /usr/local/tomcat/
RUN mv  apache-tomcat-7.0.57 tomcat

RUN  cp -rf tomcat/* ./ && rm -rf tomcat bin/*.bat

#change server config:utf-8 ,time zone
RUN rm -rf /usr/local/tomcat/conf/server.xml
ADD server.xml /usr/local/tomcat/conf/
RUN cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime

#add vim(some time will can not success ,please try again)
RUN apt-get update
RUN apt-get -y --force-yes install vim

#new relic
ADD 1yd-newrelic-java-3.14.0.zip /usr/local/tomcat/

RUN unzip 1yd-newrelic-java-3.14.0.zip && rm 1yd-newrelic-java-3.14.0.zip &&  java -jar newrelic/newrelic.jar install


EXPOSE 8080

CMD ["catalina.sh", "run"]
