FROM ubuntu:14.04
MAINTAINER Bahmni Team <bahmni@thoughtworks.com>
ENV REFRESHED_AT 2015-02-16T07:17

RUN apt-get -yqq update
RUN apt-get -yqq install tomcat7 default-jdk wget unzip

ENV CATALINA_HOME /usr/share/tomcat7
ENV CATALINA_BASE /var/lib/tomcat7
ENV CATALINA_PID /var/run/tomcat7.pid
ENV CATALINA_SH /usr/share/tomcat7/bin/catalina.sh
ENV CATALINA_TMPDIR /tmp/tomcat7-tomcat7-tmp

RUN mkdir -p $CATALINA_TMPDIR

ADD setup-artifacts.sh /tmp/setup-artifacts.sh

RUN chmod +x /tmp/setup-artifacts.sh

ADD reports.properties /tmp/reports.properties

RUN /tmp/setup-artifacts.sh web

ADD openmrs-runtime.properties /root/.OpenMRS/openmrs-runtime.properties

ADD bahmnicore.properties /root/.OpenMRS/bahmnicore.properties

ADD setupDbAndStart.sh /root/.OpenMRS/setupDbAndStart.sh

RUN chmod 777 /root/.OpenMRS/setupDbAndStart.sh

RUN chown -R root:root /root/.OpenMRS

ADD run-liquibase-migrations.sh /tmp/run-liquibase-migrations.sh

VOLUME [ "/var/lib/tomcat7/webapps/" ]

VOLUME [ "/root/.OpenMRS/modules" ]

VOLUME [ "/root/.OpenMRS/obscalculator" ]

VOLUME [ "/root/.OpenMRS/encounterModifier" ]

EXPOSE 8080

EXPOSE 8000

ENTRYPOINT [ "/root/.OpenMRS/setupDbAndStart.sh" ]