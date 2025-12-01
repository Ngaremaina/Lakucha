FROM ubuntu:latest
LABEL authors="ngare"

# Stage 1: Build the .jar
FROM maven:3.9.6-eclipse-temurin-21 AS build

WORKDIR /app

# Copy only pom.xml first to leverage Docker layer caching
COPY pom.xml .

# Now copy the full source
COPY . .

# Build the application
RUN mvn clean install -DskipTests

# Stage 2: Run the jar
FROM eclipse-temurin:21-jdk

WORKDIR /app

COPY --from=build /app/target/backend-0.0.1-SNAPSHOT.jar /app/backend.jar

EXPOSE 8080

CMD ["java", "-jar", "/app/backend.jar"]