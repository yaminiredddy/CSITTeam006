# Software Design Description (SDD)

## 1. Introduction

### 1.1 Purpose
The purpose of this Software Design Description (SDD) is to provide a detailed design for the Pinterest clone application. This document describes the software's architecture, components, interfaces, and their interactions to ensure that the implementation meets the system's functional and non-functional requirements.

### 1.2 Scope
The Pinterest clone system enables users to discover, save, and share visual content via a mobile app. Users can create boards, pin images, and explore content shared by others. The system includes the mobile application, backend API services, image processing, real-time communication, and external integration with services like cloud storage and email gateways.

## 4. Module Design

### 4.1 Mobile Application (Frontend)

#### 4.1.1 User Interface (UI)
The UI is designed to be simple, visually appealing, and easy to use. The UI components include:
- Home Screen
- Explore Screen
- Board Management Screen
- Pin Detail Screen
- User Profile Screen

#### 4.1.2 Controller Layer
Manages user requests and communicates with the service layer for processing. This includes:
- Pin Management Controller
- Authentication Controller
- Board Management Controller

#### 4.1.3 Service Layer
Handles business logic like pin creation, board management, and user interactions.

### 4.2 Backend System (Server-side)

#### 4.2.1 API Gateway
The API Gateway serves as the entry point for all mobile application requests. It forwards requests to appropriate backend services.

#### 4.2.2 Authentication Service
Handles:
- User registration
- User login
- Password recovery and reset

#### 4.2.3 Pin Management Service
Handles:
- **Pin Creation**: Users create new pins with images and descriptions.
- **Board Management**: Users can create and manage boards to organize pins.
- **Content Discovery**: Algorithms to recommend pins based on user interests.

#### 4.2.4 Image Processing Service
Manages:
- Image upload and storage using external cloud storage services.
- Image resizing and optimization for different devices.

#### 4.2.5 Notification Service
Responsible for sending notifications to users about activities like new followers, comments, and likes.

## 5. Database Design

The Pinterest clone uses a NoSQL database (e.g., MongoDB). Below is the database schema for major entities. 
![image](https://github.com/user-attachments/assets/85da26f9-89e7-4719-9938-0bf8f63b1d46)



### Explanation:
- **Users**: Stores user details like name, email, preferences.
- **Pins**: Stores pin-related information like image URL, description, and tags.
- **Boards**: Stores details about boards, including the user's pins and board descriptions.
- **Notifications**: Stores notification details for user activities.

## 6. Interface Design

### 6.1 API Design
Below are some of the REST API endpoints for interaction:

- `POST /api/auth/register`: User registration
- `POST /api/auth/login`: User login
- `GET /api/pins`: Retrieve pins
- `POST /api/pins`: Create a new pin
- `GET /api/boards`: Retrieve user boards
- `POST /api/boards`: Create a new board

![image](https://github.com/user-attachments/assets/10915ab9-1e14-4bd1-907a-fe7c3a029944)



### 6.2 External System Interfaces
- **Cloud Storage**: Handles image upload and storage (e.g., AWS S3, Google Cloud Storage).
- **Email Gateway**: Sends notifications and verification emails to users (e.g., SendGrid).

### 6.3 Notification Flow Diagram
This diagram represents the flow of notifications between services.

![image](https://github.com/user-attachments/assets/10fbe4e5-bf47-4ffc-bfd8-4d5670ceb87f)


## 7. Non-Functional Requirements

### 7.1 Performance
The system should handle at least 50,000 simultaneous users.

### 7.2 Scalability
The backend must be horizontally scalable to handle growth in user base and content.

### 7.3 Availability
99.9% uptime with redundancy in critical components.

### 7.4 Security
Data encryption for sensitive information and secure image storage.

## 8. Conclusion
This Software Design Description outlines the architecture, modules, database, and interfaces for the Pinterest clone system, ensuring the application is robust, scalable, and secure. The use of modular design and external system integration ensures that the system is capable of handling a large number of users and content effectively.
