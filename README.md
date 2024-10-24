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

In this project, **Domain-Driven Design (DDD)** principles are applied, which focus on encapsulating business rules and logic within the domain itself. The project also follows a **Rich Domain Model** approach, moving away from the **Anemic Domain Model**, to ensure that business logic is directly embedded in entities and value objects.

Additionally, **Strongly Typed IDs** are used to improve type safety and prevent ID-related bugs, ensuring that each entity is identified with specific, strongly typed value objects rather than primitive data types.

The project also implements **Domain Events** to decouple different parts of the domain logic, allowing various parts of the system to react to changes within the domain in a flexible and scalable way.

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
![baseapi_swagger](https://github.com/user-attachments/assets/38aa202a-fdcb-4cfa-86c8-2691a198d7fa)
