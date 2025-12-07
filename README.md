# Hospital Management System

An event-driven microservices application for managing hospital operations including patient registration and appointment scheduling.

## Architecture

The system consists of:
- **API Gateway**: Routes requests to microservices (Port 8080)
- **Auth Service**: Handles authentication and authorization (Port 8083)
- **Patient Service**: Manages patient registration (Port 8081)
- **Appointment Service**: Manages appointment scheduling (Port 8082)
- **React Client**: Frontend web application (Port 3000)
- **Apache Kafka**: Event bus for asynchronous communication
- **PostgreSQL**: Database for each microservice

## Prerequisites

- Java 17 or higher
- Maven 3.8+
- Node.js 18+ and npm
- Docker and Docker Compose

## Getting Started

### 1. Start Infrastructure Services

Start Kafka, Zookeeper, and PostgreSQL databases:

```bash
docker-compose up -d
```

### 2. Build Backend Services

Build all microservices:

```bash
mvn clean install
```

### 3. Run Backend Services

Run each service in a separate terminal:

```bash
# API Gateway
cd api-gateway
mvn spring-boot:run

# Auth Service
cd auth-service
mvn spring-boot:run

# Patient Service
cd patient-service
mvn spring-boot:run

# Appointment Service
cd appointment-service
mvn spring-boot:run
```

### 4. Run Frontend

Install dependencies and start the React application:

```bash
cd react-client
npm install
npm run dev
```

The application will be available at http://localhost:3000

## Testing

### Run Unit Tests

```bash
mvn test
```

### Run Property-Based Tests

```bash
mvn test -Dtest=**/*PropertyTest
```

### Run Integration Tests

```bash
mvn verify
```

### Run Frontend Tests

```bash
cd react-client
npm test
```

## API Endpoints

### Auth Service (via API Gateway)
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login and get JWT token
- `POST /api/auth/refresh` - Refresh access token

### Patient Service (via API Gateway)
- `POST /api/patients` - Register new patient
- `GET /api/patients/{id}` - Get patient by ID
- `GET /api/patients` - List all patients

### Appointment Service (via API Gateway)
- `POST /api/appointments` - Schedule appointment
- `GET /api/appointments/{id}` - Get appointment by ID
- `GET /api/appointments/doctor/{doctorId}` - Get doctor's schedule

## Development

### Code Coverage

Generate code coverage report:

```bash
mvn jacoco:report
```

View reports at `target/site/jacoco/index.html` in each service directory.

### Stop Infrastructure

```bash
docker-compose down
```

To remove volumes:

```bash
docker-compose down -v
```

## Technology Stack

**Backend:**
- Spring Boot 3.2.0
- Spring Cloud Gateway
- Spring Data JPA
- Spring Kafka
- PostgreSQL
- Flyway (Database Migrations)
- JUnit 5 + Mockito
- jqwik (Property-Based Testing)
- Testcontainers

**Frontend:**
- React 18
- Vite
- React Router
- React Query
- Axios
- Tailwind CSS
- Vitest + React Testing Library

## Project Structure

```
hospital-management-system/
├── api-gateway/           # API Gateway service
├── auth-service/          # Authentication service
├── patient-service/       # Patient management service
├── appointment-service/   # Appointment scheduling service
├── react-client/          # React frontend application
├── docker-compose.yml     # Infrastructure services
└── pom.xml               # Parent POM
```
