
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
