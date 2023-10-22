# Stage 1: Build the application
FROM maven:3.8.5-openjdk-17-slim as builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src /app/src
RUN mvn -DskipTests clean package

# Stage 2: Create a lightweight image for running the application
FROM openjdk:22-ea-17-slim
WORKDIR /app
COPY --from=builder /app/target/ng16-spring-boot*.jar api.jar
EXPOSE 8080
CMD ["java", "-jar", "api.jar"]
