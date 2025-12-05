# Spring Boot Application with CI/CD Pipeline

<div align="center">

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen?style=for-the-badge&logo=spring-boot)
![Java](https://img.shields.io/badge/Java-17+-orange?style=for-the-badge&logo=java)
![Maven](https://img.shields.io/badge/Maven-3.8+-C71A36?style=for-the-badge&logo=apache-maven)
![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?style=for-the-badge&logo=docker)
![CI/CD](https://img.shields.io/badge/CI%2FCD-Automated-success?style=for-the-badge&logo=github-actions)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

*Enterprise-grade Spring Boot application with fully automated CI/CD pipeline*

[Features](#features) • [Quick Start](#quick-start) • [Documentation](#documentation) • [Architecture](#architecture) • [Contributing](#contributing)

</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Running the Application](#running-the-application)
- [CI/CD Pipeline](#cicd-pipeline)
- [Testing](#testing)
- [Deployment](#deployment)
- [API Documentation](#api-documentation)
- [Monitoring & Logging](#monitoring--logging)
- [Security](#security)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🎯 Overview

This project demonstrates a production-ready Spring Boot application integrated with a comprehensive CI/CD pipeline. It showcases modern DevOps practices, containerization, automated testing, and continuous deployment strategies suitable for enterprise environments.

### Key Highlights

- **Automated Build & Deployment**: Fully automated CI/CD pipeline using GitHub Actions
- **Containerization**: Docker-based deployment for consistency across environments
- **Code Quality**: Integrated SonarQube analysis and code coverage reporting
- **Security**: Built-in security scanning and vulnerability detection
- **Scalability**: Kubernetes-ready configuration for orchestration
- **Monitoring**: Integrated observability with health checks and metrics

---

## ✨ Features

### Application Features
- ✅ RESTful API with CRUD operations
- ✅ Spring Security integration
- ✅ Database connectivity (JPA/Hibernate)
- ✅ Exception handling and validation
- ✅ API documentation with Swagger/OpenAPI
- ✅ Health checks and actuator endpoints
- ✅ Logging with SLF4J and Logback

### DevOps Features
- 🚀 Automated CI/CD with GitHub Actions
- 🐳 Docker containerization
- ☸️ Kubernetes deployment manifests
- 📊 SonarQube code quality analysis
- 🧪 Automated unit and integration testing
- 📦 Maven-based dependency management
- 🔒 Security scanning in pipeline
- 📈 Code coverage reporting (JaCoCo/Codecov)

---

## 🛠 Technology Stack

### Backend
| Technology | Version | Purpose |
|-----------|---------|---------|
| Java | 17+ | Programming Language |
| Spring Boot | 3.x | Application Framework |
| Spring Web | - | REST API Development |
| Spring Data JPA | - | Data Persistence |
| Spring Security | - | Authentication & Authorization |
| Spring Actuator | - | Monitoring & Health Checks |

### Build & Dependencies
- **Maven** 3.8+ - Build automation and dependency management
- **Maven Wrapper** - Embedded Maven for consistent builds

### Database
- **H2** (Development) - In-memory database
- **PostgreSQL/MySQL** (Production) - Relational database

### DevOps & CI/CD
- **GitHub Actions** - CI/CD orchestration
- **Docker** - Containerization
- **Kubernetes** - Container orchestration
- **SonarQube** - Code quality analysis
- **JaCoCo** - Code coverage
- **JUnit 5** - Testing framework
- **Mockito** - Mocking framework

### Deployment Options
- **AWS Elastic Beanstalk** / **EC2**
- **Azure App Service**
- **Heroku**
- **Docker Compose** (Local/Development)
- **Kubernetes** (Production)

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     CI/CD Pipeline Flow                      │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  Git Push → GitHub Actions → Build → Test → Quality Check   │
│     ↓            ↓              ↓       ↓         ↓          │
│  Trigger    Checkout Code    Maven   JUnit    SonarQube     │
│                               Build   Tests    Analysis      │
│                                 ↓       ↓         ↓          │
│                            Docker  Coverage   Security       │
│                            Build   Report     Scan          │
│                               ↓                 ↓            │
│                           Push to   Generate Artifacts      │
│                           Registry                           │
│                               ↓                              │
│                          Deploy to Environment               │
│                     (Dev → Staging → Production)            │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### Application Architecture

```
┌──────────────────────────────────────────────────────────┐
│                    Spring Boot Application                │
├──────────────────────────────────────────────────────────┤
│                                                            │
│  ┌─────────────┐      ┌──────────────┐                  │
│  │   REST      │      │   Service    │                  │
│  │ Controllers │─────▶│   Layer      │                  │
│  └─────────────┘      └──────────────┘                  │
│         │                     │                           │
│         │                     ▼                           │
│         │            ┌──────────────┐                    │
│         │            │ Repository   │                    │
│         │            │   Layer      │                    │
│         │            └──────────────┘                    │
│         │                     │                           │
│         ▼                     ▼                           │
│  ┌──────────────────────────────┐                       │
│  │        Database (JPA)        │                       │
│  └──────────────────────────────┘                       │
│                                                           │
│  Cross-cutting Concerns:                                 │
│  • Security (Authentication/Authorization)               │
│  • Exception Handling                                    │
│  • Logging & Monitoring                                  │
│  • Validation                                            │
│                                                           │
└───────────────────────────────────────────────────────────┘
```

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Java Development Kit (JDK)** 17 or higher
  ```bash
  java -version
  ```

- **Maven** 3.8+ (or use the included Maven Wrapper)
  ```bash
  mvn -version
  ```

- **Docker** (for containerization)
  ```bash
  docker --version
  ```

- **Git** (for version control)
  ```bash
  git --version
  ```

- **IDE** (recommended):
  - IntelliJ IDEA
  - Eclipse
  - VS Code with Java extensions

---

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/bhupal2027/Spring_boot_APP_CI-CD.git
cd Spring_boot_APP_CI-CD
```

### 2. Configure Application Properties

Edit `src/main/resources/application.properties`:

```properties
# Server Configuration
server.port=8080
spring.application.name=spring-boot-cicd-app

# Database Configuration (H2 for development)
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# JPA Configuration
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

# Actuator Configuration
management.endpoints.web.exposure.include=health,info,metrics
management.endpoint.health.show-details=always

# Logging Configuration
logging.level.root=INFO
logging.level.com.yourpackage=DEBUG
```

### 3. Build the Project

Using Maven Wrapper (recommended):
```bash
./mvnw clean install
```

Or using installed Maven:
```bash
mvn clean install
```

### 4. Run Tests

```bash
./mvnw test
```

---

## ▶️ Running the Application

### Local Development

#### Option 1: Using Maven
```bash
./mvnw spring-boot:run
```

#### Option 2: Using Java
```bash
java -jar target/spring-boot-cicd-app-1.0.0.jar
```

#### Option 3: Using Docker

Build the Docker image:
```bash
docker build -t spring-boot-cicd-app:latest .
```

Run the container:
```bash
docker run -p 8080:8080 spring-boot-cicd-app:latest
```

#### Option 4: Using Docker Compose
```bash
docker-compose up -d
```

### Verify Application

Once running, access the application:
- **Application**: http://localhost:8080
- **Health Check**: http://localhost:8080/actuator/health
- **API Documentation**: http://localhost:8080/swagger-ui.html

---

## 🔄 CI/CD Pipeline

### GitHub Actions Workflow

The CI/CD pipeline is defined in `.github/workflows/ci-cd.yml` and includes:

#### 1. **Continuous Integration**
```yaml
# Triggered on push/pull request to main branch
- Checkout code
- Set up JDK 17
- Cache Maven dependencies
- Build with Maven
- Run unit tests
- Run integration tests
- Generate code coverage report
- SonarQube analysis
- Security vulnerability scan
```

#### 2. **Continuous Deployment**
```yaml
# Triggered on successful CI build
- Build Docker image
- Tag with version and commit SHA
- Push to Docker registry
- Deploy to development environment
- Deploy to staging (on merge to develop)
- Deploy to production (on release tag)
```

### Pipeline Stages

```
┌─────────────┐    ┌──────────┐    ┌────────────┐    ┌─────────┐
│   Build     │───▶│   Test   │───▶│  Quality   │───▶│ Deploy  │
│             │    │          │    │   Check    │    │         │
│ • Compile   │    │ • Unit   │    │ • SonarQ   │    │ • Dev   │
│ • Package   │    │ • Integr │    │ • Coverage │    │ • Stage │
│             │    │          │    │ • Security │    │ • Prod  │
└─────────────┘    └──────────┘    └────────────┘    └─────────┘
```

### Environment Variables Required

Set these secrets in GitHub repository settings:

```bash
DOCKER_USERNAME          # Docker Hub username
DOCKER_PASSWORD          # Docker Hub password/token
SONAR_TOKEN             # SonarQube authentication token
AWS_ACCESS_KEY_ID       # AWS credentials (if deploying to AWS)
AWS_SECRET_ACCESS_KEY   # AWS secret key
KUBE_CONFIG            # Kubernetes config (if deploying to K8s)
```

### Manual Deployment

To manually trigger deployment:

```bash
# Login to Docker
docker login

# Build and push
docker build -t yourusername/spring-boot-cicd-app:v1.0.0 .
docker push yourusername/spring-boot-cicd-app:v1.0.0

# Deploy to Kubernetes
kubectl apply -f k8s/deployment.yml
kubectl apply -f k8s/service.yml
```

---

## 🧪 Testing

### Test Structure

```
src/test/java/
├── unit/               # Unit tests
│   ├── controller/
│   ├── service/
│   └── repository/
├── integration/        # Integration tests
│   └── api/
└── e2e/               # End-to-end tests
```

### Running Tests

```bash
# Run all tests
./mvnw test

# Run specific test class
./mvnw test -Dtest=UserControllerTest

# Run with coverage
./mvnw clean test jacoco:report

# View coverage report
open target/site/jacoco/index.html
```

### Test Coverage Goals
- **Line Coverage**: > 80%
- **Branch Coverage**: > 70%
- **Method Coverage**: > 85%

---

## 🚢 Deployment

### Docker Deployment

#### Dockerfile
```dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

#### Docker Compose
```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=prod
    depends_on:
      - db
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: appdb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
```

### Kubernetes Deployment

#### Deployment Manifest
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: spring-boot-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: spring-boot-app
  template:
    metadata:
      labels:
        app: spring-boot-app
    spec:
      containers:
      - name: app
        image: yourusername/spring-boot-cicd-app:latest
        ports:
        - containerPort: 8080
```

### Cloud Platforms

#### AWS Elastic Beanstalk
```bash
eb init -p java-17 spring-boot-cicd-app
eb create spring-boot-env
eb deploy
```

#### Heroku
```bash
heroku create spring-boot-cicd-app
git push heroku main
heroku open
```

---

## 📚 API Documentation

### Swagger/OpenAPI

Access interactive API documentation at:
```
http://localhost:8080/swagger-ui.html
```

### Sample API Endpoints

#### Health Check
```bash
GET /actuator/health
```

#### Example CRUD Operations
```bash
# Create
POST /api/users
Content-Type: application/json
{
  "name": "John Doe",
  "email": "john@example.com"
}

# Read All
GET /api/users

# Read One
GET /api/users/{id}

# Update
PUT /api/users/{id}

# Delete
DELETE /api/users/{id}
```

---

## 📊 Monitoring & Logging

### Application Metrics

Access actuator endpoints:
```bash
# Health status
curl http://localhost:8080/actuator/health

# Application metrics
curl http://localhost:8080/actuator/metrics

# Application info
curl http://localhost:8080/actuator/info
```

### Logging Configuration

Logs are configured in `src/main/resources/logback-spring.xml`:

```xml
<configuration>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>
    
    <root level="INFO">
        <appender-ref ref="STDOUT" />
    </root>
</configuration>
```

### Monitoring Tools Integration

- **Prometheus**: Metrics collection
- **Grafana**: Visualization dashboards
- **ELK Stack**: Centralized logging
- **New Relic/DataDog**: APM monitoring

---

## 🔒 Security

### Security Features

- ✅ Spring Security integration
- ✅ JWT-based authentication
- ✅ Role-based access control (RBAC)
- ✅ CORS configuration
- ✅ SQL injection prevention
- ✅ XSS protection
- ✅ CSRF protection
- ✅ Security headers

### Vulnerability Scanning

```bash
# OWASP Dependency Check
./mvnw dependency-check:check

# Snyk security scan
snyk test

# Trivy container scan
trivy image spring-boot-cicd-app:latest
```

### Best Practices

1. Never commit sensitive data (use environment variables)
2. Keep dependencies updated
3. Use HTTPS in production
4. Implement rate limiting
5. Regular security audits

---

## ⚙️ Configuration

### Application Profiles

#### Development (`application-dev.properties`)
```properties
spring.profiles.active=dev
debug=true
logging.level.root=DEBUG
```

#### Production (`application-prod.properties`)
```properties
spring.profiles.active=prod
server.port=8080
spring.datasource.url=${DATABASE_URL}
```

### Environment Variables

```bash
# Database
DATABASE_URL=jdbc:postgresql://localhost:5432/mydb
DATABASE_USERNAME=user
DATABASE_PASSWORD=password

# Application
SPRING_PROFILES_ACTIVE=prod
SERVER_PORT=8080
JWT_SECRET=your-secret-key
```

---

## 🔧 Troubleshooting

### Common Issues

#### Issue: Port 8080 already in use
```bash
# Find process using port 8080
lsof -i :8080
# Kill the process
kill -9 <PID>
```

#### Issue: Maven build fails
```bash
# Clean and rebuild
./mvnw clean install -U
```

#### Issue: Docker container won't start
```bash
# Check container logs
docker logs <container-id>

# Inspect container
docker inspect <container-id>
```

#### Issue: Database connection fails
- Verify database is running
- Check connection string in `application.properties`
- Ensure correct credentials
- Check firewall/network settings

### Debug Mode

Run in debug mode:
```bash
./mvnw spring-boot:run -Dspring-boot.run.arguments=--debug
```

---

## 🤝 Contributing

We welcome contributions! Please follow these steps:

### 1. Fork the Repository
```bash
git clone https://github.com/yourusername/Spring_boot_APP_CI-CD.git
```

### 2. Create a Feature Branch
```bash
git checkout -b feature/your-feature-name
```

### 3. Make Your Changes
- Follow code style guidelines
- Add tests for new features
- Update documentation

### 4. Run Tests
```bash
./mvnw clean test
```

### 5. Commit Your Changes
```bash
git add .
git commit -m "feat: add new feature"
```

Follow [Conventional Commits](https://www.conventionalcommits.org/):
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `test:` Test updates
- `refactor:` Code refactoring

### 6. Push and Create Pull Request
```bash
git push origin feature/your-feature-name
```

### Code Review Process
1. Automated tests must pass
2. Code review by maintainers
3. SonarQube quality gate must pass
4. Merge to main branch


## 📞 Contact & Support

### Project Maintainer
- **Name**: Bhupal
- **Email**: kotlabhupalreddy3443@gmail.com
- **GitHub**: [@bhupal2027](https://github.com/bhupal2027)
- **LinkedIn**: https://www.linkedin.com/in/kotlabhupalreddy/

## 🙏 Acknowledgments

- Spring Boot Team for the excellent framework
- GitHub Actions for CI/CD infrastructure
- SonarQube for code quality analysis
- Docker for a containerization platform
- All contributors who helped improve this project

**Made with ❤️ by Bhupal**

If you found this project helpful, please give it a ⭐!

[⬆ Back to Top](#spring-boot-application-with-cicd-pipeline)

</div>
