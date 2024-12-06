# Software Design Description (SDD)

## 1. Introduction

### 1.1 Purpose
The purpose of this Software Design Description (SDD) is to provide a detailed design for the Pinterest clone application. This document describes the software's architecture, components, interfaces, and their interactions to ensure that the implementation meets the system's functional and non-functional requirements.

### 1.2 Scope
The Pinterest clone system enables users to discover, save, and share visual content via a mobile app. Users can create boards, pin images, and explore content shared by others. The system includes the mobile application, backend API services, image processing, real-time communication, and external integration with services like cloud storage and email gateways.
### 1.3 Overview
This document outlines the system's architecture, data design, components, and human interface. It also includes design rationales, data flow descriptions, and requirements traceability.

### 1.4 Reference Material
- IEEE Std 1016-2009: Software Design Descriptions
- Pinterest Clone System Requirements Specification (SRS)

### 1.5 Definitions and Acronyms
- **API**: Application Programming Interface
- **JWT**: JSON Web Token
- **SRS**: Software Requirements Specification
- **SDD**: Software Design Document
- **NoSQL**: Non-Relational Database

## 2. System Overview
The Pinterest Clone application is a mobile and web platform enabling users to discover, save, and share visual content. The system incorporates user authentication, personalized recommendations, and content organization. It integrates with cloud storage for image hosting and offers real-time notifications for user interactions like comments, likes, and follows.

## 3. Architecture Design

### 3.1 Architecture Components

#### **User Interfaces**

##### Mobile App (Frontend)
- **Home Screen**: Displays recommended pins and boards.
- **Explore Screen**: Allows users to discover content based on categories and tags.
- **Board Management Screen**: Enables users to create and manage boards.
- **Pin Detail Screen**: Provides details of a selected pin.
- **User Profile Screen**: Displays user details, boards, and activity.

#### **Backend System**
- **API Gateway**: Acts as the single entry point for requests, routing them to appropriate backend services.
- **Authentication Service**: Handles user registration, login, and password recovery.
- **Pin Management Service**: Manages pin creation, updates, and recommendations.
- **Image Processing Service**: Optimizes and stores uploaded images using external cloud storage.
- **Notification Service**: Sends notifications for activities like comments, likes, and new followers.

#### **Admin Dashboard**
- **User Management**: Allows the admin to manage users (suspend accounts, resolve issues).
- **Content Moderation**: Enables moderation of pins and boards flagged by users.
- **Analytics Dashboard**: Provides insights into user activity, popular content, and system performance.

### 3.2 Backend Services

#### **Authentication**
- Secure login and token-based authentication using JWT.
- Manages user roles and permissions.

#### **Pin and Board Management**
- Handles the lifecycle of pins, including creation, updates, and deletion.
- Organizes content into boards and allows user collaboration on shared boards.
- Implements recommendation algorithms for personalized content discovery.

#### **Image Processing and Storage**
- Optimizes images for faster loading.
- Integrates with cloud storage services like AWS S3 or Google Cloud Storage.

#### **Real-time Notifications**
- WebSocket-based communication for real-time updates (e.g., likes, comments).
- Push notifications for mobile alerts.

### 3.3 Databases

#### **NoSQL Database (MongoDB)**
- Stores structured data like user profiles, pins, boards, and notifications.

#### **Redis**
- Caches frequently accessed data such as recommended pins and user sessions.

### 3.4 External APIs

- **Cloud Storage APIs**: For image upload and retrieval (e.g., AWS S3, Google Cloud Storage).
- **Email Gateway APIs**: For sending verification emails and activity notifications (e.g., SendGrid, Postmark).
- **Analytics APIs**: For user behavior tracking and insights (e.g., Google Analytics).

### 3.5 Infrastructure

#### **Hosting**
- Uses cloud platforms like AWS or Google Cloud for backend services and databases.

#### **Load Balancer**
- Distributes traffic across multiple servers using tools like AWS ELB or Nginx.

#### **Monitoring Tools**
- Prometheus and Grafana for tracking performance and uptime.
- Log aggregation using tools like Elasticsearch and Kibana.

#### **CI/CD Pipeline**
- Automates deployments using GitHub Actions or Jenkins.
- Includes automated testing and rollback mechanisms for reliability.

### 3.6 Workflow Overview

1. **User Interactions**
   - User browses content, pins images, or creates boards via the mobile app.
2. **Request Processing**
   - The API Gateway forwards requests to the appropriate backend service.
3. **Content Management**
   - Pins are processed, stored, and made available for discovery.
4. **Real-time Notifications**
   - Users are notified of likes, comments, and follower activities in real-time.
5. **Admin Oversight**
   - Admin dashboard monitors content, user activity, and system performance.

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
