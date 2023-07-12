# Start with a base image containing Java runtime and Maven
FROM maven:3.8.1-openjdk-17-slim AS build

# Make source directory
RUN mkdir -p /server

# Set the current working directory in the image
WORKDIR /server

# Copy pom.xml
COPY pom.xml /server

# Copy the source code
COPY src /server/src

# Package the application
RUN mvn -f pom.xml clean package

# Start with a base image containing Java runtime
FROM openjdk:17-jdk-slim

# Add Maintainer Info
LABEL maintainer="mail@winson.dev"

# Set the current working directory in the image
WORKDIR /app

# Copy the jar from the build stage
COPY --from=build /server/target/backend-0.0.1-SNAPSHOT.jar /app/app.jar
EXPOSE 9090
# Run the jar file 
ENTRYPOINT ["java","-jar","/app/app.jar"]
