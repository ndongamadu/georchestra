FROM jetty:9.3-jre8

ENV XMS=512M XMX=1G

RUN java -jar "$JETTY_HOME/start.jar" --add-to-startd=jmx,jmx-remote,stats

ADD . /

# Temporary switch to root
USER root

RUN chown jetty:jetty /etc/georchestra

# Restore jetty user
USER jetty

VOLUME [ "/tmp" ]

CMD ["sh", "-c", "exec java \
-Djava.io.tmpdir=/tmp/jetty \
-Dgeorchestra.datadir=/etc/georchestra \
-Xms$XMS -Xmx$XMX \
-XX:-UsePerfData \
${JAVA_OPTIONS} \
-jar /usr/local/jetty/start.jar"]
