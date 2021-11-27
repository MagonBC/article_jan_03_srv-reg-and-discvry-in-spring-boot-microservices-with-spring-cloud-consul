FROM docker.io/adoptopenjdk/openjdk11:latest
RUN  groupadd spring && useradd spring -g spring
USER spring:spring
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
