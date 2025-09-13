# Dockerization of Python Django Application

This project demonstrates how to containerize a Django web application using Docker and Docker Compose. The main focus is on showing the complete dockerization process for a multi-service application with a database.

## Project Purpose

This repository serves as a **demonstration of Docker containerization** for:
- A Python Django web application
- MySQL database integration
- Multi-container orchestration with Docker Compose
- Development and production-ready containerization practices

## Application Overview

A simple Django todo list application that includes:
- User authentication system
- Todo list management
- REST API endpoints
- Multi-app Django structure

## Technologies Used

- **Python 3.8** - Application runtime
- **Django 4.1.10** - Web framework
- **MySQL** - Database
- **Docker** - Containerization platform
- **Docker Compose** - Multi-container orchestration

## Docker Architecture

This project demonstrates containerization using:

### Main Application Container (`Dockerfile`)
- **Base Image**: Python 3.8
- **Multi-stage build** for optimization
- **Dependencies**: Installed from `requirements.txt`
- **Auto-migration**: Runs Django migrations on startup
- **Port**: Exposed on 8080

### Database Container (`Dockerfile.mysql`)
- **Base Image**: MySQL latest
- **Environment variables** for database configuration
- **Volume mounting** for data persistence
- **Port**: Exposed on 3306

### Docker Compose Configuration
- **Networking**: Custom network `todoapp-net`
- **Service dependencies**: App depends on MySQL
- **Volume management**: Persistent data storage
- **Environment configuration**: Database credentials and settings

## Key Dockerization Files

```
├── Dockerfile              # Python application container
├── Dockerfile.mysql        # MySQL database container  
├── docker-compose.yml      # Multi-container orchestration
└── requirements.txt        # Python dependencies
```

## How to Run the Dockerized Application

### Prerequisites
- Docker
- Docker Compose

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/zave52/dockerization-python-app.git
   cd dockerization-python-app
   ```

2. **Build and run with Docker Compose**
   ```bash
   docker-compose up --build
   ```

3. **Access the application**
   - Application: http://localhost:8080
   - Database: localhost:3306

4. **Stop the application**
   ```bash
   docker-compose down
   ```

## Docker Features Demonstrated

### 1. Multi-stage Build (Dockerfile)
```dockerfile
FROM python:3.8 as builder
# Build stage

FROM python:3.8 as run  
# Runtime stage
```

### 2. Environment Variables
- Database configuration through environment variables
- Python unbuffered output for better logging

### 3. Volume Management
- Persistent MySQL data storage
- Volume mapping for database files

### 4. Network Configuration
- Custom Docker network for service communication
- Service name resolution (app connects to `mysql` host)

### 5. Service Dependencies
- Application waits for database to be ready
- Proper startup order with `depends_on`

### 6. Port Mapping
- Application: `8080:8080`
- Database: `3306:3306`

## License

This project is licensed under the GNU General Public License v3.0 - see the LICENSE file for details.