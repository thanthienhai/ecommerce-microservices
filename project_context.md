# Project Context: Micro Marketplace - E-commerce Microservices

## 1. Project Overview

Micro Marketplace is a robust e-commerce application built on a microservices architecture using Spring technologies and open-source tools. This comprehensive system demonstrates modern distributed system patterns with full observability, security, and resilience features.

**Project Purpose:** 
- Showcase microservices architecture patterns
- Implement modern Spring Cloud ecosystem
- Demonstrate event-driven communication
- Provide comprehensive observability and monitoring
- Establish secure authentication and authorization

**Current Version:** 1.0-SNAPSHOT  
**Primary Language:** Java 17  
**Architecture Type:** Microservices with Event-Driven Communication

## 2. Technology Stack

- **Language**: Java 17
- **Framework**: Spring Boot 3.1.3, Spring Cloud 2022.0.4
- **Build Tool**: Maven
- **Containerization**: Docker, Docker Compose, Jib
- **CI/CD**: Docker-based deployment
- **Service Discovery**: Netflix Eureka
- **API Gateway**: Spring Cloud Gateway
- **Security**: Keycloak OAuth 2.0
- **Circuit Breaker**: Resilience4j
- **Message Broker**: Apache Kafka
- **Observability**: Micrometer, Zipkin, Prometheus, Grafana
- **Databases**: MongoDB (Product Service), MySQL (Order & Inventory Services)

## 3. Architecture Overview

Micro Marketplace follows a **distributed microservices architecture** with the following key characteristics:

### 3.1 Service Mesh Pattern
- Each business domain is isolated into independent microservices
- Services communicate via REST APIs and asynchronous messaging
- Service discovery enables dynamic service location
- API Gateway provides unified entry point

### 3.2 Event-Driven Architecture
- Apache Kafka handles asynchronous communication
- Order placement triggers notification events
- Loose coupling between services via event streaming

### 3.3 Observability-First Design
- Distributed tracing across all service calls
- Comprehensive metrics collection
- Centralized logging and monitoring
- Real-time dashboards and alerting

## 4. Main Modules

1. **Product Service**: MongoDB-based product catalog management
2. **Order Service**: MySQL-based order processing with circuit breaker patterns
3. **Inventory Service**: MySQL-based stock management with real-time updates
4. **Notification Service**: Kafka-based event-driven notification system
5. **API Gateway**: Centralized routing, security, and load balancing
6. **Discovery Server**: Eureka-based service registry and discovery

## 5. Pipeline Workflow

### 5.1 Main Data Flow
```
Client Request → API Gateway → Service Discovery → Target Service → Database
                     ↓
            Security Validation (Keycloak)
                     ↓
            Circuit Breaker (Resilience4j)
                     ↓
            Distributed Tracing (Zipkin)
```

### 5.2 Event Flow
```
Order Creation → Inventory Check → Order Persistence → Kafka Event → Notification Service
```

### 5.3 Monitoring Flow
```
Service Metrics → Prometheus → Grafana Dashboard
Service Traces → Zipkin → Distributed Tracing UI
```

## 6. Environments

- **Development**: Local Docker Compose setup
  - All services run in containers
  - Ports: API Gateway (8181), Discovery Server (8761), Keycloak (8080)
  - Monitoring: Prometheus (9090), Grafana (3000), Zipkin (9411)

- **Container Orchestration**: Docker Compose
  - Service interdependencies managed
  - Network isolation and communication
  - Volume persistence for databases

- **Production Ready Features**:
  - Health checks and monitoring
  - Circuit breaker patterns
  - Distributed tracing
  - Security with OAuth 2.0

## 7. Key Dependencies

### Core Spring Dependencies
- `spring-boot-starter-web`: REST API development
- `spring-boot-starter-data-jpa`: Database integration
- `spring-boot-starter-data-mongodb`: MongoDB integration
- `spring-cloud-starter-netflix-eureka-client`: Service discovery
- `spring-cloud-starter-gateway`: API Gateway functionality

### Resilience & Monitoring
- `resilience4j-spring-boot3`: Circuit breaker, retry, timeout
- `micrometer-tracing-bridge-brave`: Distributed tracing
- `zipkin-reporter-brave`: Zipkin integration
- `micrometer-registry-prometheus`: Metrics collection

### Messaging & Security
- `spring-kafka`: Apache Kafka integration
- `spring-security-oauth2-resource-server`: OAuth 2.0 resource server
- `testcontainers`: Integration testing with containers

### External Services
- **Keycloak**: Authentication server (spring-boot-microservices-realm)
- **Apache Kafka**: Message broker (notificationTopic)
- **MongoDB**: Product database
- **MySQL**: Order and Inventory databases
- **Prometheus**: Metrics collection
- **Grafana**: Visualization and dashboards
- **Zipkin**: Distributed tracing

## 8. Quick Start Guide

### Prerequisites
- Docker and Docker Compose installed
- Minimum 8GB RAM recommended
- Ports 3000, 8080, 8181, 8761, 9090, 9411 available

### Step 1: Clone and Navigate
```bash
git clone <repository-url>
cd ecommerce-microservices
```

### Step 2: Start All Services
```bash
docker compose up -d
```

### Step 3: Verify Services
```bash
docker ps
```

### Step 4: Access Components
- **API Gateway**: http://localhost:8181
- **Eureka Dashboard**: http://localhost:8761
- **Keycloak Admin**: http://localhost:8080 (admin/admin)
- **Prometheus**: http://localhost:9090
- **Grafana**: http://localhost:3000 (admin/password)
- **Zipkin**: http://localhost:9411

### Step 5: Test APIs
1. Get OAuth token from Keycloak
2. Use token to access protected endpoints:
   - `POST /api/product` - Create products
   - `GET /api/product` - List products
   - `POST /api/order` - Place orders

### Step 6: Monitor and Observe
- View service discovery in Eureka
- Monitor metrics in Prometheus
- Visualize dashboards in Grafana
- Trace requests in Zipkin

### Development Commands
```bash
# Build individual service
mvn clean compile -pl product-service

# Run tests
mvn test

# Build Docker images
mvn compile jib:dockerBuild

# View logs
docker logs <container-name>
```

This microservices platform provides a comprehensive foundation for building scalable, resilient, and observable e-commerce applications with modern cloud-native patterns.
