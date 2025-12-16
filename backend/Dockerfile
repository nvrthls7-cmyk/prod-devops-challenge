FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

FROM eclipse-temurin:17-jre
WORKDIR /app

# Copy app and set ownership using numeric UID:GID
COPY --from=build --chown=10001:10001 /app/target/*.jar app.jar

# Run as non-root numeric user (portable)
USER 10001

EXPOSE 8085
ENTRYPOINT ["java","-jar","app.jar"]