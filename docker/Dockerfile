FROM openjdk:8u151-jdk-alpine3.7

EXPOSE 8091

ENV APP_HOME /usr/src/app

COPY target/*.jar $APP_HOME/app.jar

WORKDIR $APP_HOME

ENTRYPOINT ["java","-jar","app.jar"]
