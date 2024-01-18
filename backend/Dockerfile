#FROM gradle:jdk17 AS build
#RUN mkdir -p /app
#WORKDIR /workspace
#COPY .. .
#RUN gradle bootJar --no-daemon

#FROM openjdk:17-alpine
#WORKDIR /app
#COPY --from=build /workspace/build/libs/*.jar app.jar
#CMD ["java", "-jar", "app.jar","spring-boot:run"]/
FROM openjdk:17-jdk-alpine
ENV PORT 9091
EXPOSE 9091
COPY build/libs/*.jar /opt/app.jar
WORKDIR /opt
CMD ["java", "-jar", "app.jar"]
