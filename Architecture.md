
![WhatsApp Image 2024-12-05 at 00 05 53_a80094ae](https://github.com/user-attachments/assets/8a3e2486-d147-43c6-b631-8dd3385ed9b4)

@startuml
skinparam style strictuml

package "Pinterest-like Application" {
    class User {
        +id: int
        +username: String
        +email: String
        +password: String
        +createBoard(name: String): Board
        +followUser(user: User): void
    }

    class Board {
        +id: int
        +name: String
        +owner: User
        +pins: List<Pin>
        +addPin(pin: Pin): void
    }

    class Pin {
        +id: int
        +image: String
        +description: String
        +url: String
        +addToBoard(board: Board): void
    }

    class Notification {
        +id: int
        +content: String
        +user: User
        +send(): void
    }

    class Comment {
        +id: int
        +content: String
        +user: User
        +pin: Pin
    }

    User "1" --> "0..*" Board : creates
    Board "0..*" --> "1..*" Pin : contains
    Pin "0..*" --> "1" Board : belongs to
    Pin "1..*" --> "0..*" Comment : has
    User "0..*" --> "0..*" User : follows
    User "0..*" --> "0..*" Notification : receives
}
@enduml

![image](https://github.com/user-attachments/assets/b9327abc-a5dd-47e3-b8ea-bbedfd6c86bb)

@startuml
!define RECTANGLE class

package "Pinterest Clone Application" {
    [Mobile Application] <<Mobile Application>> 
    [Web Application] <<Web Application>> 
    [User API Gateway] <<API Gateway>> 
    [User Service] <<Microservice>> 
    [Board Service] <<Microservice>> 
    [Pin Service] <<Microservice>> 
    [Notification Service] <<Microservice>> 

    [User Database] <<Database>> 
    [Board Database] <<Database>> 
    [Pin Database] <<Database>> 
    [Notification System] <<External System>> 

    [Mobile Application] --> [User API Gateway] : API Calls
    [Web Application] --> [User API Gateway] : API Calls
    [User API Gateway] --> [User Service] : Manage Users
    [User API Gateway] --> [Board Service] : Manage Boards
    [User API Gateway] --> [Pin Service] : Manage Pins
    [User API Gateway] --> [Notification Service] : Send Notifications
    [User Service] --> [User Database] : Read/Write Data
    [Board Service] --> [Board Database] : Read/Write Data
    [Pin Service] --> [Pin Database] : Read/Write Data
    [Notification Service] --> [Notification System] : Push Notifications
}
@enduml

Deployment Diagram Code
![image](https://github.com/user-attachments/assets/9082dddd-27b5-4380-a55c-c96164394cc6)


@startuml
!define RECTANGLE class

package "Pinterest Clone Application" {
    [Mobile Application] <<Mobile Application>> 
    [Web Application] <<Web Application>> 
    [User API Gateway] <<API Gateway>> 
    [User Service] <<Microservice>> 
    [Board Service] <<Microservice>> 
    [Pin Service] <<Microservice>> 
    [Notification Service] <<Microservice>> 

    [User Database] <<Database>> 
    [Board Database] <<Database>> 
    [Pin Database] <<Database>> 
    [Notification System] <<External System>> 

    [Mobile Application] --> [User API Gateway] : API Calls
    [Web Application] --> [User API Gateway] : API Calls
    [User API Gateway] --> [User Service] : Manage Users
    [User API Gateway] --> [Board Service] : Manage Boards
    [User API Gateway] --> [Pin Service] : Manage Pins
    [User API Gateway] --> [Notification Service] : Send Notifications
    [User Service] --> [User Database] : Read/Write Data
    [Board Service] --> [Board Database] : Read/Write Data
    [Pin Service] --> [Pin Database] : Read/Write Data
    [Notification Service] --> [Notification System] : Push Notifications
}
@enduml




