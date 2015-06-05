FROM maven:3.2-jdk-6

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME

ENV TOMCAT_MAJOR 6
ENV TOMCAT_VERSION 6.0.43
#HOME ,vim will err if not
ENV HOME /root

#you can get at http://mirror.cogentco.com/pub/apache/tomcat/tomcat-6/v6.0.43/bin/apache-tomcat-6.0.43.tar.gz
# install tomcat
ADD apache-tomcat-6.0.43.tar.gz /usr/local/tomcat/
RUN mv  apache-tomcat-6.0.43 tomcat

RUN  cp -rf tomcat/* ./ && rm -rf tomcat bin/*.bat

#change server config:utf-8 ,time zone  
RUN rm -rf /usr/local/tomcat/conf/server.xml
ADD server.xml /usr/local/tomcat/conf/
RUN echo "Asia/Shanghai" > /etc/timezone && \
        dpkg-reconfigure -f noninteractive tzdata

#new relic
ADD 1yd-newrelic-java-3.14.0.zip /usr/local/tomcat/

RUN unzip 1yd-newrelic-java-3.14.0.zip && rm 1yd-newrelic-java-3.14.0.zip &&  java -jar newrelic/newrelic.jar install

EXPOSE 8080

CMD ["catalina.sh","run"]
