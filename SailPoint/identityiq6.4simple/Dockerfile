FROM redhat/ut-rhel6-tom7jre8

MAINTAINER Rick Huff <rhuff@austin.utexas.edu>

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
WORKDIR $CATALINA_HOME

RUN mkdir -p $CATALINA_HOME/webapps/identityiq 
#
# Update the timezone.
# 
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/US/Central /etc/localtime

#
# Patch the OS.
#
RUN yum update -y 

#
# Install SailPoint: This requires a configured SailPoint in the identityiq directory.
#
COPY identityiq $CATALINA_HOME/webapps/identityiq
COPY server.xml $CATALINA_HOME/conf/server.xml
COPY tomcat-users.xml $CATALINA_HOME/conf/tomcat-users.xml

EXPOSE 8009
CMD ["catalina.sh", "run"]
# CMD /bin/bash
