FROM gradle:jdk17 AS build
RUN mkdir -p /app
WORKDIR /workspace
COPY . .
RUN gradle bootJar --no-daemon

FROM openjdk:17-alpine
WORKDIR /app
COPY --from=build /workspace/build/libs/*.jar app.jar
CMD ["java", "-jar", "app.jar"]
