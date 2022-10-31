FROM maven:3.5-jdk-8-alpine

WORKDIR /code

COPY . .

RUN mvn package -D skipTests

CMD java -jar target/worker-jar-with-dependencies.jar
