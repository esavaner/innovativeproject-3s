FROM maven:3.5.2-jdk-8-alpine AS MAVEN_BUILD

WORKDIR /server
COPY . .
RUN mvn -Dmaven.test.skip=true package

FROM openjdk:8-jdk-alpine

WORKDIR /server
#.jar file name depends on pom.xml project.build.finalName property, eg. <finalName>SpringApp</finalName>
COPY --from=MAVEN_BUILD /server/target/server-0.0.1-SNAPSHOT.jar ./

RUN apk update  \
 && apk add  docker 

EXPOSE 8080
CMD java -jar ./server-0.0.1-SNAPSHOT.jar