# Docker DevOps Lab

This repository contains the deliverables for the Docker DevOps lab, demonstrating core DevOps principles and practices with Docker and Spring Boot.

## Lab Objectives

- Understand core DevOps principles and practices
- Build and run Docker images
- Create Dockerfiles for application containerization
- Define and run multi-container applications using Docker Compose

## Contents

1. A simple Spring Boot application
2. Dockerfile for containerizing the Spring Boot application
3. Docker Compose file for a multi-container setup

## Prerequisites

- Java JDK 11 or later
- Maven
- Docker
- Docker Compose

## Setup and Running

### Building the Spring Boot Application

1. Navigate to the project root directory
2. Run the following command:
   ```
   mvn clean package
   ```

### Building and Running the Docker Image

1. Build the Docker image:
   ```
   docker build -t springboot-docker .
   ```
2. Run the Docker container:
   ```
   docker run -p 8080:8080 springboot-docker
   ```

### Running the Multi-Container Application

1. Navigate to the directory containing the `docker-compose.yml` file
2. Run the following command:
   ```
   docker-compose up
   ```

## Project Structure

```
.
├── src/                    # Source files for the Spring Boot application
├── Dockerfile              # Dockerfile for building the application image
├── docker-compose.yml      # Docker Compose file for multi-container setup
├── pom.xml                 # Maven configuration file
└── README.md               # This file
```

## Exercises Completed

1. Created a simple Dockerfile for a Spring Boot application
2. Built and ran the Docker image
3. Defined a multi-container application using Docker Compose (web app, redis, database)
4. Deployed the multi-container application using Docker Compose

## Contributing

This project is part of a lab exercise. Contributions, issues, and feature requests are welcome for educational purposes.

## License

[None]
