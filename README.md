# Online Soccer Field Booking System

A microservices-based online soccer field booking platform built with Golang. This system allows users to browse available soccer fields, check schedules, make bookings, and process payments seamlessly.

## 🏗️ Architecture

This project follows a microservices architecture pattern with the following services:

### Services Overview

1. **User Service** - Manages user authentication and authorization
2. **Field Service** - Handles field management and scheduling
3. **Order Service** - Processes booking orders and manages order history
4. **Payment Service** - Integrates with payment gateway (Midtrans) for payment processing

### Infrastructure Components

-   **Kafka** - Message broker for inter-service communication
-   **PostgreSQL** - Primary database for all services
-   **Zookeeper** - Kafka cluster coordination
-   **PgAdmin** - Database management interface
-   **Kafka UI** - Kafka cluster monitoring and management

## 📁 Project Structure

```
backend/
├── docker-compose.yml              → Main infrastructure setup
├── user-service-main/              → User authentication & management
├── field-service-main/             → Field & schedule management
├── order-service-main/             → Order processing & history
└── payment-service-main/           → Payment gateway integration
```

### Service Directory Structure

Each service follows a clean architecture pattern:

```
service/
├── clients/                        → HTTP clients for inter-service communication
├── cmd/                            → Application entry point
├── common/                         → Shared utilities and helpers
│   ├── error/                      → Error handling utilities
│   ├── response/                   → Response formatting
│   └── util/                       → Common utilities
├── config/                         → Configuration management
│   ├── config.go                   → App configuration
│   └── database.go                 → Database configuration
├── constants/                      → Application constants
├── controllers/                    → Request handlers
├── domain/                         → Business domain
│   ├── dto/                        → Data Transfer Objects
│   └── models/                     → Database models
├── middlewares/                    → HTTP middlewares (auth, logging, etc.)
├── repositories/                   → Data access layer
├── routes/                         → API route definitions
├── services/                       → Business logic layer
├── config.json.example             → Configuration template
├── docker-compose.yaml             → Service-specific Docker setup
├── Dockerfile                      → Service container definition
├── go.mod                          → Go module dependencies
├── Jenkinsfile                     → CI/CD pipeline configuration
├── Makefile                        → Build and development commands
└── README.md                       → Service documentation
```

## 🚀 Getting Started

### Prerequisites

-   Go 1.22.0 or higher
-   Docker & Docker Compose
-   Make (optional, for using Makefile commands)
-   PostgreSQL (if running without Docker)

### Installation

1. **Clone the repository**

    ```bash
    git clone <repository-url>
    cd backend
    ```

2. **Start infrastructure services**

    ```bash
    docker-compose up -d
    ```

    This will start:

    - PostgreSQL (port 5432)
    - PgAdmin (port 5050)
    - Kafka (port 9092)
    - Zookeeper (port 2181)
    - Kafka UI (port 8070)

3. **Set up each microservice**

    For each service directory (`user-service-main`, `field-service-main`, `order-service-main`, `payment-service-main`):

    ```bash
    cd <service-directory>

    # Install dependencies
    go mod tidy

    # Copy configuration files
    cp config.json.example config.json
    # Edit config.json with your settings

    # (Optional) If using Consul
    cp .env.example .env
    # Edit .env with your settings
    ```

4. **Configure each service**

    Edit the `config.json` file in each service with appropriate database and service configurations.

## 🏃 Running the Services

### Option 1: Run with Docker (Recommended)

Each service can be run with Docker:

```bash
cd <service-directory>
docker-compose up -d --build --force-recreate
```

### Option 2: Run Locally with Hot Reload

For development with hot reload:

```bash
cd <service-directory>

# First time setup or when adding new dependencies
make watch-prepare

# Start with hot reload
make watch
```

### Option 3: Build and Run

```bash
cd <service-directory>

# Build the service
make build

# Run the built binary
./<service-name>
```

## 🔧 Infrastructure Access

After running `docker-compose up -d`:

-   **PostgreSQL Database**: `localhost:5432`

    -   Username: `root`
    -   Password: `barca1899`

-   **PgAdmin**: http://localhost:5050

    -   Email: `admin@pgadmin.com`
    -   Password: `admin`

-   **Kafka**: `localhost:9092`
-   **Kafka UI**: http://localhost:8070
-   **Zookeeper**: `localhost:2181`

## 📡 API Endpoints

Each service exposes its own REST API. Refer to individual service README files for detailed API documentation:

-   [User Service API](./user-service-main/README.md)
-   [Field Service API](./field-service-main/README.md)
-   [Order Service API](./order-service-main/README.md)
-   [Payment Service API](./payment-service-main/README.md)

## 🛠️ Technology Stack

-   **Language**: Go 1.22.0
-   **Web Framework**: Gin
-   **ORM**: GORM
-   **Database**: PostgreSQL
-   **Message Queue**: Apache Kafka
-   **Payment Gateway**: Midtrans
-   **Cloud Storage**: Google Cloud Storage (GCS)
-   **Service Discovery**: Consul (optional)
-   **Logging**: Logrus
-   **Containerization**: Docker
-   **CI/CD**: Jenkins

## 📦 Key Dependencies

-   `github.com/gin-gonic/gin` - HTTP web framework
-   `gorm.io/gorm` - ORM library
-   `gorm.io/driver/postgres` - PostgreSQL driver
-   `github.com/google/uuid` - UUID generation
-   `github.com/sirupsen/logrus` - Structured logging
-   `cloud.google.com/go/storage` - Google Cloud Storage
-   `github.com/didip/tollbooth` - Rate limiting
-   `github.com/spf13/viper` - Configuration management

## 🔄 Development Workflow

1. **Make changes** to the service code
2. **Run tests** (if available)
3. **Build** using `make build`
4. **Test locally** using `make watch` for hot reload
5. **Commit** changes
6. **CI/CD pipeline** (Jenkins) will handle deployment

## 🧪 Testing

Run tests for each service:

```bash
cd <service-directory>
go test ./...
```

## 🐛 Debugging

-   Check service logs in Docker:

    ```bash
    docker-compose logs -f <service-name>
    ```

-   Access Kafka UI to monitor message queues: http://localhost:8070
-   Use PgAdmin to inspect database state: http://localhost:5050

## 📝 Configuration

Each service uses `config.json` for configuration. Example structure:

```json
{
    "server": {
        "port": 8080,
        "host": "localhost"
    },
    "database": {
        "host": "localhost",
        "port": 5432,
        "user": "root",
        "password": "barca1899",
        "dbname": "service_db"
    },
    "kafka": {
        "brokers": ["localhost:9092"]
    }
}
```

## 🤝 Contributing

1. Create a feature branch
2. Make your changes
3. Write/update tests
4. Submit a pull request

## 📄 License

[MIT License](LICENSE)

## 🔗 Related Links

-   [Gin Documentation](https://gin-gonic.com/)
-   [GORM Documentation](https://gorm.io/)
-   [Apache Kafka](https://kafka.apache.org/)
-   [Docker Documentation](https://docs.docker.com/)

---

For detailed information about individual services, please refer to their respective README files in each service directory.
