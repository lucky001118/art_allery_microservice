## Art Gallery Microservices - Config Server

This repository contains the configuration server for the **Art Gallery** application, an e-commerce platform for buying and selling art. The Config Server centralizes and manages configuration for all the microservices in the system, ensuring a consistent and seamless deployment process.

---

## Features

- Centralized configuration management for all services in the Art Gallery application.
- Secure access to configuration properties.
- Dynamic updates to configurations without restarting services.
- Support for multiple environments (e.g., `development`, `staging`, `production`).
- Integration with a service registry (Eureka Server) for seamless communication.

---

## Prerequisites

Before running the Config Server, ensure that:

1. **Git** is installed and accessible on the host system.
2. The **`art_gallery_microservice`** repository is available on GitHub, containing configuration files for the application.
3. A **Spring Boot Config Server** project is set up.

---

## Configuration Repository Structure

The external repository for configurations (`art_gallery_microservice`) should follow this structure:

```
art_gallery_microservice
├── application.yml
├── service-registry.yml
├── gateway.yml
├── user-service.yml
├── admin-service.yml
├── seller-service.yml
├── customer-service.yml
└── other-service.yml
```

Each file represents the configuration for a specific microservice.

---

## Environment Setup

The `application.yml` in the Config Server project should include:

```yaml
server:
  port: 8888 # Default port for the Config Server

spring:
  application:
    name: config-server
  cloud:
    config:
      server:
        git:
          uri: https://github.com/<your-username>/art_gallery_microservice
          default-label: main # Branch name in the repository
  profiles:
    active: native # Use `native` for testing local configurations
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
  instance:
    hostname: localhost
  fetch-registry: true
  register-with-eureka: true
```

> Replace `<your-username>` with your GitHub username.

---

## Running the Config Server

1. Clone the Config Server repository:
   ```bash
   git clone https://github.com/<your-username>/config-server.git
   cd config-server
   ```

2. Build and run the application:
   ```bash
   ./mvnw spring-boot:run
   ```

3. Verify the server is running at `http://localhost:8888`.

---

## Accessing Configuration Files

Configuration files can be accessed using the following URL patterns:

- **Default configuration**:  
  `http://localhost:8888/{application}/{profile}`

- **Specific branch**:  
  `http://localhost:8888/{application}/{profile}/{branch}`

For example:
- To fetch the `development` profile for the `user-service`:  
  `http://localhost:8888/user-service/development`

---

## Service Registry Integration

The Config Server integrates with the Service Registry (Eureka Server) to allow seamless discovery by other microservices. Ensure that the Eureka Server is running at `http://localhost:8761`.

### Eureka Configuration

```yaml
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
  instance:
    hostname: config-server
  fetch-registry: true
  register-with-eureka: true
```

---

## Security

For production, consider enabling the following:

1. **Encrypting sensitive configuration values** using Spring Cloud Config's encryption features.
2. **Securing the Config Server endpoints** using Spring Security.

---

## Contact

For queries or support, reach out to the project maintainer at **[your-email@example.com](mailto:manikpurilucky218@gmail.com)**.
```

Make sure to customize the content based on your specific project structure and details. Let me know if you'd like additional details!
