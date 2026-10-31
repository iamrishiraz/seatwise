# Seatwise

A scalable, fault-tolerant ticket reservation system built with Spring Boot, Redis, and PostgreSQL. This system is designed to handle concurrent ticket reservations, ensuring each ticket can only be reserved once, even under high load.

## 🚀 Features

- **Distributed Locking**: Uses Redis and Redisson for distributed locking to prevent race conditions during ticket reservations
- **Scalable Architecture**: Horizontally scalable with load balancing via Nginx
- **Database Persistence**: PostgreSQL for reliable data storage
- **Containerized**: Fully dockerized for easy deployment and scaling
- **Monitoring**: Includes metrics endpoints with Prometheus integration
- **Transaction Management**: ACID-compliant transactions for data integrity

## 🏗️ Architecture

![Architecture Diagram](static/img.png)

The system is built with a microservices architecture:

- **Multiple Application Instances**: Horizontally scalable application nodes
- **Nginx Load Balancer**: Distributes traffic across application instances
- **Redis**: Provides distributed locking mechanism
- **PostgreSQL**: Stores ticket and reservation data

## 🔧 Tech Stack

- **Backend**: Java 17, Spring Boot 3.1.3
- **Database**: PostgreSQL 14
- **Caching & Locking**: Redis with Redisson
- **Load Balancing**: Nginx
- **Containerization**: Docker & Docker Compose
- **Monitoring**: Micrometer with Prometheus integration

## 🚦 Getting Started

### Prerequisites

- Docker and Docker Compose
- Java 17 (for development)
- Gradle (or use the included wrapper)

### Running Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/iamrishiraz/seatwise.git
cd seatwise
   ```

2. Start the application using Docker Compose:
   ```bash
   docker-compose up -d
   ```

3. The application will be accessible at:
    - API Endpoint: http://localhost:80
    - Individual instances: http://localhost:8081 and http://localhost:8082
    - PostgreSQL: localhost:5432
    - Redis: localhost:6379

### API Endpoints

- `POST /api/tickets/{ticketId}/reserve` - Reserve a ticket
- `POST /api/tickets/{ticketId}/release` - Release a ticket reservation
- `GET /actuator/health` - Health check
- `GET /actuator/metrics` - Metrics information
- `GET /actuator/prometheus` - Prometheus metrics

### Docker Configuration

Docker Compose is used to manage and connect the different services. See `docker-compose.yml` for details.

## 🧪 Testing

### Unit Tests

Run unit tests with:

```bash
./gradlew test
```

### Integration Tests

Integration tests use TestContainers to spin up real PostgreSQL and Redis instances:

```bash
./gradlew integrationTest
```

### Load Testing

A concurrent test script is included to simulate high loads:

```bash
./test-concurrent.sh
```

## 🔒 Distributed Locking

The core of this system is the distributed locking mechanism implemented with Redisson. This ensures that:

1. Each ticket can only be reserved once
2. Race conditions are prevented when multiple users try to reserve the same ticket
3. Locks are released properly even if a service instance fails




## 📈 Monitoring

The application exposes various metrics via Spring Boot Actuator and Prometheus integration. You can:

1. Check the health endpoint: `/actuator/health`
2. View metrics: `/actuator/metrics`
3. Scrape Prometheus metrics: `/actuator/prometheus`

## 🔍 Troubleshooting

### Common Issues

1. **Redis Connection Failure**:
    - Ensure Redis is running and accessible from application containers
    - Check `REDIS_HOST` and `REDIS_PORT` environment variables

2. **Database Connection Issues**:
    - Verify PostgreSQL is running
    - Check database credentials in environment variables

3. **Load Balancer Issues**:
    - Ensure Nginx configuration is correctly pointing to application instances
    - Verify both application instances are healthy


## 👥 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.