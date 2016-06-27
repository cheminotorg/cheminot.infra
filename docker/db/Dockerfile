FROM debian:8.3

MAINTAINER Sebastien Renault <srenault.contact@gmail.com>

RUN apt-get -y update && apt-get -y upgrade

RUN apt-get -y install wget

RUN apt-get -y install apt-transport-https ca-certificates

# OPENJDK

RUN apt-get -y install openjdk-7-jre

# NEO4J

RUN wget -O - https://debian.neo4j.org/neotechnology.gpg.key | apt-key add -

RUN echo 'deb http://debian.neo4j.org/repo stable/' > /tmp/neo4j.list

RUN mv /tmp/neo4j.list /etc/apt/sources.list.d

RUN echo "deb https://apt.dockerproject.org/repo debian-jessie main" >> /etc/apt/sources.list.d/backports.list

RUN apt-get -y update

RUN apt-get -y --force-yes install docker-engine

RUN apt-get -y install neo4j=2.3.1

# BUILD DB

WORKDIR /db

RUN wget https://www.dropbox.com/s/n3jbkaw2bgrbg09/cheminotcli-latest.jar?dl=1 -O cheminotcli.jar

RUN java -jar ./cheminotcli.jar --out /db

# ENTRYPOINT

WORKDIR /app

RUN wget https://raw.githubusercontent.com/cheminotorg/cheminot.infra/master/deploy/neo4j -O neo4j

RUN chmod +x ./neo4j

CMD ["--path", "/db/current/world/cheminot.db", "--auth", "false", "--https", "false"]

ENTRYPOINT ["/app/neo4j"]
