# 🏭 PostgreSQL Foreign Data Wrapper OpenAPI Service

[![.NET](https://img.shields.io/badge/.NET-6.0-512BD4?logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![ASP.NET Core](https://img.shields.io/badge/ASP.NET%20Core-6.0-512BD4?logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/apps/aspnet)
[![Entity Framework Core](https://img.shields.io/badge/EF%20Core-6.0-512BD4?logo=dotnet&logoColor=white)](https://docs.microsoft.com/ef/core/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-FDW-336791?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-D24939?logo=jenkins&logoColor=white)](https://www.jenkins.io/)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![OpenAPI](https://img.shields.io/badge/OpenAPI-3.0-6BA539?logo=openapi-initiative&logoColor=white)](https://swagger.io/specification/)

Enterprise ASP.NET Core API service providing unified access to multi-source databases through PostgreSQL Foreign Data Wrapper (FDW) with comprehensive OpenAPI documentation and automated CI/CD pipeline.

## 📖 **Overview**

The PostgreSQL FDW OpenAPI Service is an enterprise-grade data warehouse solution that provides unified RESTful API access to heterogeneous data sources through PostgreSQL Foreign Data Wrapper technology. Built with ASP.NET Core 6.0, it enables seamless integration of manufacturing data across multiple database systems.

## 🏗️ **Architecture**

```text
┌─────────────────────────────────────────────────────────────┐
│                    External Data Sources                    │
├─────────────────┬─────────────────┬─────────────────────────┤
│     Oracle      │    SQL Server   │       MySQL             │
│                 │                 │                         │
│ Manufacturing   │ Business Logic  │ Legacy Systems          │
│ Execution       │ Applications    │ Historical Data         │
└─────────────────┴─────────────────┴─────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│              PostgreSQL Foreign Data Wrapper                │
├─────────────────────────────────────────────────────────────┤
│  • Oracle FDW        • SQL Server FDW                       │
│  • MySQL FDW         • File-based FDW                       │
│  • Unified Schema    • Data Type Mapping                    │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                ASP.NET Core Web API                         │
├─────────────────────────────────────────────────────────────┤
│  • RESTful Endpoints    • OpenAPI Documentation             │
│  • Entity Framework    • Data Validation                    │
│  • Response Caching    • Error Handling                     │
└─────────────────────────────────────────────────────────────┘
```

## ⚡ **Key Features**

### 🔄 **Multi-Source Data Integration**

- **PostgreSQL FDW**: Unified access to Oracle, SQL Server, MySQL databases
- **Real-time Queries**: Live data access without ETL overhead
- **Schema Abstraction**: Simplified data model across heterogeneous sources
- **Performance Optimization**: Query optimization and result caching

### 📊 **RESTful API Services**  

- **Factory Data APIs**: Real-time manufacturing process information
- **Multiple Formats**: JSON, CSV, XML data export capabilities
- **OpenAPI Documentation**: Comprehensive Swagger UI integration
- **API Versioning**: Backward compatibility and evolution support

### 🛠️ **Enterprise Features**

- **Structured Logging**: NLog-based daily log rotation and management
- **CI/CD Integration**: Automated Jenkins pipeline deployment
- **Docker Support**: Containerized deployment for scalability
- **Error Handling**: Robust exception management and API responses

## ⚙️ **CI/CD Pipeline with Jenkins**

The FDW API includes a fully automated CI/CD pipeline using Jenkins for continuous integration and deployment:

- **Automated Building**: Automatic compilation and testing on code commits
- **Quality Gates**: Code analysis and test coverage validation  
- **Containerization**: Docker image building and registry push
- **Deployment**: Automated deployment to staging and production environments

**Jenkins Pipeline URL**: `{JENKINS_URL}/job/FDW_OpenAPI/`

## 🚀 **API Usage Examples**

### **📋 Get Process Information List**

Retrieve all available manufacturing process information.

**Request:**

```bash
GET /v1/rtls/processinfo

curl -X 'GET' \
  '{OPENAPI_BASE_URL}/v1/rtls/processinfo' \
  -H 'accept: application/json'
```

**Response:**

```http
HTTP/1.1 200 OK
api-supported-versions: 1
content-type: application/json; charset=utf-8
date: Tue, 09 May 2023 00:25:07 GMT
server: Kestrel
transfer-encoding: chunked

{
  "data": [
    {
      "processId": "PROC001",
      "location": "Line A",
      "status": "Running",
      "lastUpdate": "2023-05-09T00:25:00Z"
    }
  ]
}
```

### **🎯 Get Specific Process Data**

Retrieve detailed information for a specific manufacturing process.

**Request:**

```bash
GET /v1/rtls/processinfo/{process_loc}

curl -X 'GET' \
  '{OPENAPI_BASE_URL}/v1/rtls/processinfo/LineA' \
  -H 'accept: application/json'
```

**Response:**

```http
HTTP/1.1 200 OK
api-supported-versions: 1
content-type: application/json; charset=utf-8
date: Tue, 09 May 2023 00:32:27 GMT
server: Kestrel
transfer-encoding: chunked

{
  "processId": "PROC001",
  "location": "LineA", 
  "status": "Running",
  "metrics": {
    "efficiency": 95.2,
    "throughput": 150.5,
    "quality": 98.8
  },
  "lastUpdate": "2023-05-09T00:32:00Z"
}
```

### **📥 File Export Capabilities**

Download process information in various formats (JSON, CSV, XML).

**Request:**

```bash
GET /v1/rtls/processinfo.json

curl -X 'GET' \
  '{OPENAPI_BASE_URL}/v1/rtls/processinfo.json' \
  -H 'accept: application/octet-stream' \
  --output processinfo.json
```

**Response:**

```http
HTTP/1.1 200 OK
api-supported-versions: 1
content-disposition: attachment; filename=processinfo_list.json; filename*=UTF-8''processinfo_list.json
content-length: 13252
content-type: application/json
date: Thu, 11 May 2023 00:05:30 GMT
server: Kestrel
```

## 📚 **OpenAPI Documentation**

The FDW API provides comprehensive interactive documentation through Swagger UI:

![Swagger UI](./img/swagger.png)

### **Available Endpoints:**

- `GET /v1/rtls/processinfo` - List all manufacturing processes
- `GET /v1/rtls/processinfo/{id}` - Get specific process details  
- `GET /v1/rtls/processinfo.{format}` - Export data in JSON/CSV/XML
- `GET /v1/health` - API health check endpoint

## 📝 **Logging & Monitoring**

Advanced logging capabilities with NLog integration for comprehensive system monitoring:

![Log History](./img/LogHist.png)

### **Logging Features:**

- **Structured Logging**: JSON-formatted logs with contextual information
- **Daily Rotation**: Automatic log file rotation and archival
- **Error Tracking**: Detailed exception logging with stack traces
- **Performance Metrics**: Request/response time tracking
- **Audit Trail**: Complete API usage history

## 🏗️ **Project Structure**

```text
fdw-api/
├── 📊 CSG.DAO/                      # Data Access Objects
│   ├── Repositories/                # Repository pattern implementations
│   └── Interfaces/                  # DAO interface definitions
├── 📦 CSG.DTO/                      # Data Transfer Objects
│   ├── Request/                     # API request models
│   ├── Response/                    # API response models
│   └── Mapping/                     # AutoMapper profiles
├── 🧠 DataWarehouse.BLL/            # Business Logic Layer
│   ├── Services/                    # Business service implementations
│   ├── Validators/                  # Input validation logic
│   └── Processors/                  # Data processing components
├── 🗄️ DataWarehouse.EF/             # Entity Framework Core
│   ├── Contexts/                    # Database contexts
│   ├── Entities/                    # Entity models
│   ├── Configurations/              # Entity configurations
│   └── Migrations/                  # Database migrations
├── 🌐 DataWarehouse.OpenApi/        # ASP.NET Core Web API
│   ├── Controllers/                 # API controllers
│   ├── Middleware/                  # Custom middleware
│   ├── Infrastructure/              # API infrastructure
│   └── Extensions/                  # Service extensions
├── 🧪 DataWarehouse.OpenApi.Test/   # Unit & Integration Tests
│   ├── Controllers/                 # Controller tests
│   ├── Services/                    # Service tests
│   └── Integration/                 # Integration tests
├── 🔧 DataWarehouse.PerfAPIAnalyzer/# Performance Analysis Tool
└── 📋 DataWarehouse.sln             # Visual Studio Solution
```

## 🛠️ **Technology Stack**

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Framework** | ASP.NET Core 6.0 | Web API framework |
| **ORM** | Entity Framework Core 6.0 | Database access layer |
| **Database** | PostgreSQL + FDW | Multi-source data integration |
| **Documentation** | OpenAPI 3.0 / Swagger | API documentation |
| **Logging** | NLog | Structured logging |
| **Testing** | xUnit, Moq | Unit and integration testing |
| **CI/CD** | Jenkins | Automated deployment |
| **Containerization** | Docker | Application packaging |

## 🚀 **Quick Start**

### **Prerequisites**

- .NET 6.0 SDK or later
- PostgreSQL with FDW extensions
- Docker (optional)

### **Development Setup**

1. **Clone the repository**

   ```bash
   git clone https://github.com/codingnanyong/fdw-api.git
   cd fdw-api
   ```

2. **Configure database connections**

   ```bash
   # Update appsettings.Development.json
   {
     "FDW": {
       "HQ": {
         "ConnectionString": "Server={ip};Port={port};Database={db};Username={user};Password={password}"
       },
       "IoT": {
         "ConnectionString": "Server={ip};Port={port};Database={db};Username={user};Password={password}"
       }
     }
   }
   ```

3. **Build and run**

   ```bash
   dotnet restore
   dotnet build
   dotnet run --project DataWarehouse.OpenApi
   ```

4. **Access API documentation**
   - Swagger UI: `http://localhost:7020/swagger`
   - API Endpoints: `http://localhost:7020/api/v1/`

### **Docker Deployment**

```bash
# Build Docker image
docker build -t fdw-api .

# Run container
docker run -d -p 7020:7020 fdw-api
```

## 💡 **Use Cases**

✅ **Manufacturing Data Integration** - Unified access to production systems  
✅ **Real-time Process Monitoring** - Live manufacturing process data  
✅ **Cross-Database Analytics** - Query multiple data sources seamlessly  
✅ **Legacy System Integration** - Connect modern APIs to legacy databases  
✅ **Data Export & Reporting** - Multi-format data export capabilities  
✅ **Enterprise API Gateway** - Centralized data access layer  

## 🏆 **Production Features**

- **High Performance**: Optimized queries with result caching
- **Enterprise Security**: Authentication and authorization ready
- **Scalable Architecture**: Horizontal scaling with load balancing
- **Monitoring & Observability**: Comprehensive logging and metrics
- **API Versioning**: Backward compatibility support

## 🤝 **Contributing**

Contributions, issues, and feature requests are welcome!  
Feel free to check the [issues page](https://github.com/codingnanyong/fdw-api/issues) if you want to contribute.

### **Development Guidelines**

- Follow .NET coding standards
- Write unit tests for new features
- Update API documentation
- Ensure CI/CD pipeline passes

## 📄 **License**

This project is licensed under the MIT License. See [LICENSE](./LICENSE) for details.

---

**🏭 Enterprise Data Integration at Scale**  
Built with ❤️ for manufacturing excellence and seamless data access.
