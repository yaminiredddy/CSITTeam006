# Use Case Diagram for Pinterest

## Actors

1. **User**
   - Description: Anyone who uses Pinterest, including those who browse or create boards.

2. **Registered User**
   - Description: A User who has signed up and logged in.

3. **Admin**
   - Description: A person responsible for managing and moderating content on Pinterest.

## Use Cases

### 1. Browse Pins
- **Description**: Users can view and search for pins on Pinterest.
- **Actor**: User, Registered User

### 2. Search for Pins
- **Description**: Users can search for specific pins based on keywords or categories.
- **Actor**: User, Registered User

### 3. Create Board
- **Description**: Registered Users can create boards to organize their pins.
- **Actor**: Registered User

### 4. Pin Content
- **Description**: Registered Users can pin content to their boards.
- **Actor**: Registered User

### 5. Follow Board/Users
- **Description**: Users can follow other users or boards to see their new pins.
- **Actor**: User, Registered User

### 6. Like Pin
- **Description**: Users can like individual pins.
- **Actor**: User, Registered User

### 7. Comment on Pin
- **Description**: Users can comment on pins.
- **Actor**: User, Registered User

### 8. Edit Board
- **Description**: Registered Users can edit the boards they own.
- **Actor**: Registered User

### 9. Delete Pin
- **Description**: Registered Users can delete pins they have pinned.
- **Actor**: Registered User

### 10. Report Pin
- **Description**: Users can report inappropriate pins to the admin.
- **Actor**: User, Registered User

### 11. Manage Content
- **Description**: Admins can review and manage reported pins.
- **Actor**: Admin

### 12. Manage Users
- **Description**: Admins can manage user accounts and permissions.
- **Actor**: Admin

## Relationships

- **User** interacts with: Browse Pins, Search for Pins, Follow Board/Users, Like Pin, Comment on Pin, Report Pin
- **Registered User** interacts with: Create Board, Pin Content, Edit Board, Delete Pin, Follow Board/Users, Like Pin, Comment on Pin, Report Pin
- **Admin** interacts with: Manage Content, Manage Users

---

For a visual representation, you can use tools like Mermaid to generate diagrams. Here's an example of Mermaid syntax to include in Markdown (if supported by your Markdown renderer):

```mermaid
graph TD
    User -->|Browse Pins| Pinterest
    User -->|Search Pins| Pinterest
    User -->|Follow Board/Users| Pinterest
    User -->|Like Pin| Pinterest
    User -->|Comment on Pin| Pinterest
    User -->|Report Pin| Pinterest
    RegisteredUser -->|Create Board| Pinterest
    RegisteredUser -->|Pin Content| Pinterest
    RegisteredUser -->|Edit Board| Pinterest
    RegisteredUser -->|Delete Pin| Pinterest
    RegisteredUser -->|Follow Board/Users| Pinterest
    RegisteredUser -->|Like Pin| Pinterest
    RegisteredUser -->|Comment on Pin| Pinterest
    RegisteredUser -->|Report Pin| Pinterest
    Admin -->|Manage Content| Pinterest
    Admin -->|Manage Users| Pinterest
