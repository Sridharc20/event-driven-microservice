# Hospital Management System - Project Structure

## Overview
This document describes the complete project structure for the Hospital Management System.

## Directory Structure

```
hospital-management-system/
├── .git/                           # Git repository
├── .kiro/                          # Kiro specs and configuration
│   └── specs/
│       └── hospital-management-system/
│           ├── design.md
│           ├── requirements.md
│           └── tasks.md
├── api-gateway/                    # API Gateway Service
│   ├── src/
│   │   └── main/
│   │       └── resources/
│   │           └── application.yml
│   └── pom.xml
├── auth-service/                   # Authentication Service
│   ├── src/
│   │   └── main/
│   │       └── resources/
│   │           └── application.yml
│   └── pom.xml
├── patient-service/                # Patient Management Service
│   ├── src/
│   │   └── main/
│   │       └── resources/
│   │           └── application.yml
│   └── pom.xml
├── appointment-service/            # Appointment Scheduling Service
│   ├── src/
│   │   └── main/
│   │       └── resources/
│   │           └── application.yml
│   └── pom.xml
├── react-client/                   # React Frontend Application
│   ├── src/
│   │   ├── test/
│   │   │   └── setup.js
│   │   ├── App.jsx
│   │   ├── index.css
│   │   └── main.jsx
│   ├── .eslintrc.cjs
│   ├── index.html
│   ├── package.json
│   ├── postcss.config.js
│   ├── tailwind.config.js
│   └── vite.config.js
├── .gitignore
├── docker-compose.yml              # Infrastructure services
├── pom.xml                         # Parent POM
├── PROJECT_STRUCTURE.md            # This file
└── README.md                       # Main documentation

```

## Services Configuration

### API Gateway (Port 8080)
- Routes requests to microservices
- Handles CORS configuration
- Provides centralized error handling

### Auth Service (Port 8083)
- User authentication and JWT token generation
- User registration and management
- Password hashing with BCrypt
- Database: auth_db (PostgreSQL on port 5433)

### Patient Service (Port 8081)
- Patient registration and management
- Publishes PatientRegistered events to Kafka
- Database: patient_db (PostgreSQL on port 5432)

### Appointment Service (Port 8082)
- Appointment scheduling and management
- Consumes PatientRegistered events from Kafka
- Publishes AppointmentScheduled events to Kafka
- Database: appointment_db (PostgreSQL on port 5434)

### React Client (Port 3000)
- Frontend web application
- Built with Vite
- Uses React Router for navigation
- Uses React Query for data fetching
- Styled with Tailwind CSS

## Infrastructure Services (Docker Compose)

### Kafka (Port 9092)
- Message broker for event-driven communication
- Topics: patient.registered, appointment.scheduled

### Zookeeper (Port 2181)
- Coordination service for Kafka

### PostgreSQL Databases
- auth_db (Port 5433) - Auth Service database
- patient_db (Port 5432) - Patient Service database
- appointment_db (Port 5434) - Appointment Service database

## Technology Stack

### Backend
- Java 17
- Spring Boot 3.2.0
- Spring Cloud Gateway
- Spring Data JPA
- Spring Kafka
- Spring Security
- PostgreSQL
- Flyway (Database Migrations)
- JUnit 5 + Mockito (Unit Testing)
- jqwik (Property-Based Testing)
- Testcontainers (Integration Testing)

### Frontend
- React 18
- Vite
- React Router
- React Query
- Axios
- Tailwind CSS
- Vitest + React Testing Library

### Build Tools
- Maven 3.8+
- npm

## Next Steps

1. Start infrastructure services: `docker-compose up -d`
2. Build backend services: `mvn clean install`
3. Run individual services: `mvn spring-boot:run` in each service directory
4. Install frontend dependencies: `cd react-client && npm install`
5. Run frontend: `npm run dev`

## Testing

- Unit tests: `mvn test`
- Property-based tests: `mvn test -Dtest=**/*PropertyTest`
- Integration tests: `mvn verify`
- Frontend tests: `cd react-client && npm test`

## Code Coverage

- Minimum threshold: 80%
- Generate reports: `mvn jacoco:report`
- View reports: `target/site/jacoco/index.html` in each service
