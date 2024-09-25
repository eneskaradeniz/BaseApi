# BaseApi
It is a flexible and scalable base API project built with .NET 8 for modern web applications. The project includes key features like authentication, authorization, logging, caching, file storage, message queue, and real-time notifications.

# Technologies

* .NET 8.0
* Microsoft SQL Server
* Entity Framework 8.0
* LINQ
* MediatR
* FluentValidation
* MassTransit
* AWSSDK.S3
* Serilog / Seq
* Swagger
* Docker

# Clean Architecture
Clean architecture is a software design that suggests dependencies in the application should be one-way and point inward.

### Domain
This layer contains all entities, value objects, enums, interfaces, and domain-specific business logic. It does not depend on any other layer in the system.

### Contracts
Used to reduce dependency between layers. It includes data structures like DTOs, request-response models, which are used for communication between the Application layer.

### Application
This layer is responsible for organizing the application logic and use cases. It only depends on the Domain and Contracts layers.

It also defines extra interfaces needed to support application logic, which are implemented by the outer layers. For example, the **_IDbContext_** interface is defined in this layer but implemented by the Persistence layer.

This layer uses the **CQRS pattern** to structure the logic into commands and queries, using the MediatR library.

### Persistence
This layer handles database operations and data management. It contains EF Core configurations for entities, implements the application's database context, and sets up persistence-related dependencies.

### Infrastructure
This layer includes classes responsible for accessing external resources. These classes are based on interfaces defined in the Application layer. In the current system, it handles services like:
* Caching (Redis)
* Message Queue (RabbitMQ)
* Storage (AWS S3)
* Token (JWT)
* Email
* Cryptography

### Api
This layer brings the whole system together. Its only job is to accept HTTP requests, package them as commands or queries, send them to the appropriate part of the system for processing, and return the result as a response. Controllers are designed to be as simple and thin as possible.

# Swagger UI
![Ekran görüntüsü 2024-09-23 161804](https://github.com/user-attachments/assets/00632dd2-fbd9-4f24-ae74-b899c1933137)
