FROM maven:3.5-jdk-8-alpine

# Define variable
ARG PORT
ENV http_proxy=http://web-proxy.corp.hpecorp.net:8080
ENV https_proxy=http://web-proxy.corp.hpecorp.net:8080

WORKDIR /code

COPY . .

RUN mvn package -D skipTests -Dhttp.proxyHost=web-proxy.corp.hpecorp.net -Dhttp.proxyPort=8080 -Dhttps.proxyHost=web-proxy.corp.hpecorp.net -Dhttps.proxyPort=8080 -Dhttp.nonProxyHosts=127.0.0.1\|localhost\|.nimblestorage.com

CMD java -jar target/worker-jar-with-dependencies.jar
