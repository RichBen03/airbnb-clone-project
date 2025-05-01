# 🏡 Airbnb Clone Project

## 🚀 Overview
This project aims to develop a backend system that mimics the core functionalities of Airbnb, including user management, property listings, booking management, payments using a modern python's backend stack.

## 🏆 Project Goals
- **User Management**: Secure user registration, login, and profile handling.
- **Property Management**: Performing CRUD operations for property listings.
- **Booking System**: Allows for customer to make booking reservations, check for availability, and manage their bookings.
- **Payment Processing**: Offers secure and reliable payment handling via Payment APIs.
- **Review System**: Enables ratings and feedback for properties from customera.
- **Data Optimization**: The projct also covers indexing and caching for database optimization performance.

## ⚙️ Technology Stack

This project leverages a modern backend technology stack to deliver a scalable, secure, and high-performance application.

| Technology       | Purpose |
|------------------|---------|
| **Django**       | A high-level Python web framework used for rapid backend development, including URL routing, middleware, and ORM integration. |
| **Django REST Framework (DRF)** | An extension of Django that simplifies building and managing RESTful APIs for CRUD operations. |
| **PostgreSQL**   | A powerful open-source relational database used to store structured data such as users, properties, bookings, and payments. |
| **GraphQL**      | A flexible query language that allows clients to request exactly the data they need, reducing over-fetching and under-fetching issues. |
| **Celery**       | A task queue system used to run asynchronous tasks in the background, such as sending emails and processing payments. |
| **Redis**        | An in-memory data store used for caching, improving response times and reducing database load, as well as managing Celery task queues. |
| **Docker**       | A containerization tool that packages the application and its dependencies to ensure consistent development and deployment environments. |
| **GitHub Actions / CI/CD** | Used to automate testing, linting, and deployment pipelines, ensuring continuous integration and delivery. |



## 👥 Team Roles

To successfully deliver the Airbnb Clone backend, the following team roles are essential:

### 🔧 Backend Developer
Responsible for designing and developing RESTful and GraphQL APIs. Implements business logic, integrates third-party services such as Payment Services, manages API authentication, and ensures endpoint security.

### 🗄️ Database Administrator (DBA)
Designs the relational database schema, defines entity relationships, and optimizes database performance through indexing and normalization. HE/she also handles backup, restoration, and data security strategies.

### ⚙️ DevOps Engineer
Automates deployment pipelines, monitors infrastructure, and ensures scalable deployment using Docker, CI/CD pipelines, and cloud services. Manages version control integration and server uptime.

### 🧪 QA Engineer
Develops and executes test plans to ensure the backend performs correctly and securely. Works with automated testing tools and frameworks to detect bugs early in the development lifecycle.

### 📄 API Documentation Specialist 
Prepares and maintains accurate API documentation using OpenAPI and GraphQL standards, ensuring external developers and team members understand how to consume the APIs effectively.

### 📢 Project Manager 
Coordinates team tasks, timelines, and deliverables. He/she also manages collaboration through tools like GitHub Projects and ensures alignment with project goals and timelines.

## 🗄️ Database Design

The database is designed to support core operations like user management, property listings, bookings, reviews, and payments. Below are the key entities and their relationships:

### 1. **User**
Represents guests and hosts on the platform.
- `id`: Primary key
- `name`: Full name of the user
- `email`: Unique email address
- `password_hash`: Hashed password for secure authentication
- `is_host`: Boolean indicating if the user is a host

### 2. **Property**
Represents accommodation listings created by hosts.
- `id`: Primary key
- `user_id`: Foreign key to the User (host)
- `title`: Name of the property
- `location`: Address or city of the property
- `price_per_night`: Cost per night of stay

### 3. **Booking**
Represents reservations made by users for a property.
- `id`: Primary key
- `user_id`: Foreign key to the User (guest)
- `property_id`: Foreign key to the Property
- `start_date`: Check-in date
- `end_date`: Check-out date

### 4. **Payment**
Represents payment transactions for bookings.
- `id`: Primary key
- `booking_id`: Foreign key to the Booking
- `amount`: Total amount paid
- `payment_status`: Enum (e.g., Pending, Completed, Failed)
- `payment_date`: Date of transaction

### 5. **Review**
Represents feedback left by users after a stay.
- `id`: Primary key
- `user_id`: Foreign key to the User
- `property_id`: Foreign key to the Property
- `rating`: Integer value (1–5)
- `comment`: Textual feedback

### 6. **Relationships Summary**

- A **User** can list multiple **Properties** (`1-to-many`)  
  ↳ Hosts can own and manage many property listings.

- A **User** can make multiple **Bookings** (`1-to-many`)  
  ↳ Guests can book different properties over time.

- A **Property** can have many **Bookings** (`1-to-many`)  
  ↳ A single property may be booked by different users at different times.

- A **Booking** has one **Payment** (`1-to-1`)  
  ↳ Each reservation is linked to a single payment transaction.

- A **User** can leave many **Reviews**, each linked to one **Property** (`many-to-1`)  
  ↳ Guests can review properties they have stayed in.

- A **User** can receive Reviews as a **Host** through their Properties (`1-to-many through property`)  
  ↳ Hosts can be rated based on the properties they manage.

- A **Property** can have many **Reviews** (`1-to-many`)  
  ↳ A property accumulates feedback from various guests.

- A **User** can have both guest and host roles simultaneously  
  ↳ The same user account may book other properties while listing their own.

- A **Payment** is always associated with a **Booking**, which links it back to the **User** and **Property** (`1-to-1-to-1`)  
  ↳ Ensures traceability of who paid for what and where.

- A **Property** belongs to one **User** (the host) (`many-to-1`)  
  ↳ Every listing must be tied to a valid host account.

- A **Review** can only be posted by a **User** who completed a **Booking** for that **Property** (`many-to-1 conditional`)  
  ↳ Helps enforce authenticity in feedback.

  ### 🧩 Feature Breakdown

- **User Management**  
  Enables users to register, log in, and manage their profiles. This includes secure authentication and role-based access(customer/host), ensuring a personalized and secure user experience.

- **Property Management**  
  Hosts can create, read, update, and delete property listings with detailed descriptions and media. This system makes it easy to manage availability, pricing, and property features.

- **Booking System**  
  Users can reserve properties for specific dates, view their bookings, and manage check-ins and check-outs. It ensures availability is tracked and prevents double bookings.

- **Payment Processing**  
  Secure payment handling for completed bookings, including transaction tracking and confirmations. This supports financial trust and enables smooth monetization for hosts.

- **Review System**  
  Guests can leave reviews and ratings for properties after their stay. This builds credibility and helps future guests make informed booking decisions.

- **API Documentation (REST & GraphQL)**  
  Detailed API documentation for both REST and GraphQL ensures easy integration for frontend developers and third-party apps. It improves developer experience and project scalability.

- **Database Optimization**  
  Indexing and caching mechanisms improve data retrieval speed and reduce server load, ensuring a smooth user experience even under high traffic.

---

### 🔐 API Security

- **Authentication & Authorization**  
  JWT-based authentication will be used to verify user identity, while role-based authorization will ensure users can only access permitted resources. This protects sensitive data and enforces system boundaries.

- **Rate Limiting**  
  Limits the number of requests per IP/user to prevent abuse such as brute force attacks. This maintains service integrity and protects system resources.

- **Input Validation & Sanitization**  
  Prevents malicious data from being injected into the system (e.g., SQL Injection, XSS). This secures both client-side and server-side operations.

- **HTTPS & Secure Headers**  
  HTTPS will encrypt data in transit, while security headers like `Content-Security-Policy` and `X-Content-Type-Options` will guard against common web vulnerabilities.

- **Payment Security**  
  Ensures that transactions are processed securely, using third-party APIs (e.g., Stripe) with PCI compliance. This is vital to protect financial data and build trust.

---

### 🔄 CI/CD Pipeline

- **What is CI/CD?**  
  Continuous Integration (CI) and Continuous Deployment/Delivery (CD) automate the software development lifecycle by testing, building, and deploying code changes automatically. It helps detect bugs early and ensures smooth, frequent updates.

- **Why it Matters**  
  CI/CD improves code quality, speeds up development, reduces human error, and ensures consistent environments from development to production.

- **Tools Used**  
  - **GitHub Actions**: Automates testing, linting, and deployment workflows.  
  - **Docker**: Ensures the application runs identically across development, testing, and production environments.  
  - **Heroku/Vercel or AWS EC2**: Can be used for deploying the backend services.  
  - **PostgreSQL**: Integrated as a managed database in the CI/CD process for migrations and schema checks.


