# DTO (Data transfer object)

## Sequence Diagram

The following sequence diagram illustrates the process of fetching user data:

```mermaid
sequenceDiagram
    participant Client as Client
    participant Controller as Controller
    participant Service as Service
    participant DAL as Data Access Layer (DAL)
    participant Database as Database
    participant DTO as UserDTO

    Client ->> Controller: GET /user/123
    Controller ->> Service: GetUser(123)
    Service ->> DAL: FetchUser(123)
    DAL ->> Database: SELECT * FROM Users WHERE ID = 123
    Database -->> DAL: User data
    DAL -->> Service: Returns User Data Model
    Service ->> DTO: Map Data Model to UserDTO
    Service -->> Controller: Returns UserDTO
    Controller -->> Client: JSON response with UserDTO
```

This diagram shows the interaction between the client, controller, service, data access layer, database, and the data transfer object (DTO) when a client requests user data.
## Aggregates

Aggregates are clusters of domain objects that can be treated as a single unit. An aggregate will have one of its component objects be the aggregate root. Any references from outside the aggregate should only go to the aggregate root. The root can ensure the integrity of the aggregate as a whole.

### Example Diagram

The following diagram illustrates the relationship between an aggregate root and its entities:

```mermaid
classDiagram
    class Order {
        -orderId: int
        -orderDate: Date
        +calculateTotal(): float
    }
    class OrderItem {
        -productId: int
        -quantity: int
        -price: float
        +getTotal(): float
    }
    class Product {
        -productId: int
        -name: string
        -price: float
    }

    Order --> OrderItem : contains
    OrderItem --> Product : references
```

In this example, `Order` is the aggregate root, and it contains `OrderItem` entities. Each `OrderItem` references a `Product`.

## Repositories

Repositories are used to encapsulate the logic required to access data sources. They provide a collection-like interface for accessing domain objects.

### Example Diagram

The following diagram illustrates the interaction between a repository and the domain model:

```mermaid
sequenceDiagram
    participant Client as Client
    participant OrderRepository as OrderRepository
    participant Order as Order

    Client ->> OrderRepository: save(Order)
    OrderRepository ->> Order: validate()
    OrderRepository ->> Database: INSERT INTO Orders
    Database -->> OrderRepository: success
    OrderRepository -->> Client: success
```

This diagram shows how a client interacts with the `OrderRepository` to save an `Order` object to the database.