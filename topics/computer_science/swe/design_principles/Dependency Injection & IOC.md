---
tags:
  - cs
  - cs/swe
created: 2025-01-08T16:43
modified: 2025-08-12T12:40
published:
sources: 
topics: 
  - Dependency Injection
  - Inversion of Control
  - Design Principles
  - Object Lifecycle
authors:
ai-assisted:
hidden:
public: true
---
# Dependency Injection & IOC
(Source: ChatGPT[^1])
### Inversion of Control (IoC)
Inversion of Control is a design principle where the control flow of a program is inverted, meaning the decision of how and when a particular task is executed is delegated to a framework or external entity, rather than being managed directly by the program itself. It shifts responsibilities from the program (caller) to a container or framework, promoting flexibility and decoupling.
### Dependency Injection (DI)
Dependency Injection is a specific implementation of Inversion of Control where dependencies (objects or services that a class needs to function) are provided to a class, typically through constructors, setters, or method parameters, rather than the class creating or managing those dependencies itself. This enhances modularity, testability, and reduces tight coupling.
**Relationship:**  
Dependency Injection is a pattern that achieves Inversion of Control by outsourcing the responsibility of dependency creation and management.
## Life Cycle
In the context of **Dependency Injection (DI)** and **Inversion of Control (IoC)**, **Life Cycle** refers to how the framework or container manages the creation, configuration, use, and destruction of objects (dependencies) in an application. This management process ensures that the objects are provided when needed and disposed of appropriately.
### Object Creation Types
- [[Transient]]
	- **Lifecycle**: A new instance is created every time it is requested.
	- **Use Case**: For stateless services, ensuring no shared state or data between requests or components.
	- **Example**: Lightweight utility services like string formatters.
	- **In DI Context**: Registered as `Transient`, the IoC container creates and disposes of the instance immediately after use.
- [[Scoped]]
	- **Lifecycle**: One instance is created per HTTP request (or equivalent scope in server-side frameworks).
	- **Use Case**: For services that need to share state or data across a single request lifecycle but not beyond.
	- **Example**: Database context (e.g., `DbContext` in Entity Framework).
	- **In DI Context**: Registered as `Scoped`, the IoC container creates one instance for the request and disposes of it at the end of the request.
- [[Singleton]]
	- **Lifecycle**: A single instance is created and shared throughout the application’s lifetime.
	- **Use Case**: For expensive-to-create services or shared, global state services.
	- **Example**: Caching services, configuration providers, logging frameworks.
	- **In DI Context**: Registered as `Singleton`, the IoC container creates the instance once and reuses it across all requests and components.


[^1]: Describe to me concisely and to the point computer science concepts called inversion of control and dependency injection.