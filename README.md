# Spring Cloud Config

This repository contains a Spring Cloud Config Server implementation, which provides centralized external configuration management for distributed systems. It allows you to manage configuration properties for your microservices in a centralized and version-controlled manner.

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Clone the Repository](#clone-the-repository)
  - [Configuration](#configuration)
  - [Running the Application](#running-the-application)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Introduction

Spring Cloud Config Server is a part of the Spring Cloud ecosystem that provides a centralized configuration service for microservices. It allows you to store configuration files (e.g., `application.yml`, `application.properties`) in a version-controlled repository (like Git) and serve them to your microservices at runtime.

This project demonstrates how to set up a Spring Cloud Config Server and use it to manage configurations for your microservices.

## Features

- Centralized configuration management for microservices.
- Support for Git-based configuration repositories.
- Environment-specific configuration (e.g., `dev`, `prod`, `test`).
- Encryption and decryption of sensitive configuration properties.
- Integration with Spring Boot applications.

## Prerequisites

Before you begin, ensure you have the following installed:

- Java Development Kit (JDK) 11 or later.
- Maven 3.x or later.
- Git (for version control).
- Spring Boot 2.x or later.

## Getting Started

### Clone the Repository

To get started, clone this repository to your local machine:

```bash
git clone https://github.com/fzwnerd/springcloud-config.git
cd springcloud-config
```

### Configuration

1. **Git Repository Configuration**: 
   - Update the `application.yml` file to point to your Git repository where the configuration files are stored.
   - Example:
     ```yaml
     spring:
       cloud:
         config:
           server:
             git:
               uri: https://github.com/your-username/your-config-repo.git
               search-paths: '{application}'
     ```

2. **Environment-Specific Configuration**:
   - Create configuration files for different environments (e.g., `application-dev.yml`, `application-prod.yml`) in your Git repository.

### Running the Application

To run the Spring Cloud Config Server, use the following Maven command:

```bash
mvn spring-boot:run
```

The server will start on port `8888` by default. You can access the configuration properties by making a GET request to:

```
http://localhost:8888/{application}/{profile}
```

Where `{application}` is the name of your microservice and `{profile}` is the environment (e.g., `dev`, `prod`).

## Usage

To use the Spring Cloud Config Server in your microservices, add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

Then, configure your microservice to fetch configuration from the Config Server by adding the following to your `bootstrap.yml` or `bootstrap.properties`:

```yaml
spring:
  application:
    name: your-microservice-name
  cloud:
    config:
      uri: http://localhost:8888
```
