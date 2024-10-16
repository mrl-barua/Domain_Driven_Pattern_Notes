# DTO (Data transfer object)

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
