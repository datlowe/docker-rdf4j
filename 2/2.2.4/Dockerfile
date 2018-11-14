FROM tomcat:8.5

MAINTAINER Jan Dedek "jan.dedek@datlowe.cz"

ENV RDF4J_VERSION="2.2.4" 
ENV RDF4J_DATA="/opt/eclipse-rdf4j-${RDF4J_VERSION}/data" 
ENV JVM_PARAMS="-Xmx4g" 

RUN curl -sS -o /tmp/rdf4j.zip -L http://download.eclipse.org/rdf4j/eclipse-rdf4j-${RDF4J_VERSION}-sdk.zip && \
    unzip -j /tmp/rdf4j.zip "eclipse-rdf4j-${RDF4J_VERSION}/war/rdf4j-server.war" -d /usr/local/tomcat/webapps && \
    unzip /usr/local/tomcat/webapps/rdf4j-server.war -d /usr/local/tomcat/webapps/rdf4j-server && \
    rm /usr/local/tomcat/webapps/rdf4j-server.war && \
    rm /tmp/rdf4j.zip

COPY conf/ /usr/local/tomcat/conf/

RUN sed -i -e 's/<\/web-app>//' /usr/local/tomcat/conf/web.xml && \
	cat /usr/local/tomcat/conf/server_web_xml_security_end.xml >> /usr/local/tomcat/conf/web.xml

RUN echo "CATALINA_OPTS=\"\$CATALINA_OPTS \$JVM_PARAMS -Dorg.eclipse.rdf4j.appdata.basedir=\$RDF4J_DATA\"" >> /usr/local/tomcat/bin/setenv.sh

COPY set_sesame_pass_and_run.sh . 

CMD bash set_sesame_pass_and_run.sh run


VOLUME ${RDF4J_DATA}

EXPOSE 8080
