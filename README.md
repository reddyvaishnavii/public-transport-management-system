# 🚍 Public Transport Management System

A web-based **Public Transport Management System** developed using Java and Spring Boot as part of an Object-Oriented Analysis and Design (OOAD) mini project at PES University.

The application provides a centralized platform for managing transport operations, including user registration, route and schedule management, bus allocation, seat bookings, fare calculation, and payment processing.

Built using **Spring Boot MVC, Hibernate/JPA, and Thymeleaf**, the project demonstrates object-oriented programming principles, layered application architecture, and practical implementations of software design patterns.

---

## 🚀 Features

### 👤 User Management & Authentication
- Multi-role registration and login for passengers, administrators, drivers, and conductors.
- Role-specific dashboards and application workflows.
- Profile management and user information updates.
- User activation and deactivation functionality.
- Booking history and user management.

### 🗺️ Route & Schedule Management
- Create and manage transport routes.
- Store route details, including source, destination, and distance.
- Create and manage travel schedules.
- Search available schedules using source and destination.
- Associate buses, drivers, routes, and travel timings.
- Manage stops and their associated schedules.

### 🎟️ Booking Management
- Create and manage passenger bookings.
- Generate unique booking references.
- Track booking statuses.
- Support booking cancellation workflows.
- Maintain booking records using database persistence.

### 💰 Fare Calculation & Payment
- Calculate fares based on route distance.
- Apply additional fare adjustments for AC and peak-hour travel.
- Calculate applicable taxes.
- Calculate refunds based on cancellation timing.
- Support multiple payment strategies: Credit Card, UPI, and Digital Wallet.
- Maintain transaction records and payment statuses.

*Note: Payment processing is simulated. No external payment gateway is integrated.*

### 🚌 Fleet & Transport Administration
- Manage bus and route information.
- Assign buses and drivers to journeys.
- Create transport schedules.
- View booking and fleet information through administrative dashboards.
- Generate transport-related reports.

---

## 🛠️ Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Java 17 |
| Backend Framework | Spring Boot |
| Web Architecture | Spring MVC |
| Frontend | Thymeleaf, HTML |
| ORM | Hibernate |
| Persistence | Spring Data JPA |
| Database | H2 In-Memory Database |
| Build Tool | Apache Maven |
| Testing Framework | JUnit 5, Spring Boot Test |
| Design Tools | UML, PlantUML |
| Development Tools | IntelliJ IDEA, Git, GitHub |

---

## 🏗️ System Architecture

The application follows a layered MVC architecture to separate request handling, business logic, data persistence, and presentation.

```text
                  USER INTERFACE
                  Thymeleaf Views
                         |
                         v
                  MVC CONTROLLERS
                         |
                         v
                   SERVICE LAYER
                  Business Logic
                         |
                         v
                 REPOSITORY LAYER
                  Spring Data JPA
                         |
                         v
                    HIBERNATE
                         |
                         v
                   H2 DATABASE
```

### Architectural Components

- **Model Layer:** Defines entities such as User, Route, Bus, Schedule, Booking, Ticket, and Transaction.
- **Controller Layer:** Handles HTTP requests, user interactions, and navigation between application views.
- **Service Layer:** Implements application logic for authentication, bookings, routes, schedules, fares, and payments.
- **Repository Layer:** Handles database operations using Spring Data JPA.
- **View Layer:** Uses Thymeleaf templates to render application pages.

This separation promotes modularity, maintainability, and separation of concerns.

---

## 🎨 Object-Oriented Design & Design Patterns

The project applies object-oriented programming concepts and several design patterns to structure application components.

### OOP Principles

- **Encapsulation:** Organizes data and behavior within Java classes.
- **Inheritance:** Uses a common User base class with specialized user types such as Admin, RegularUser, DriverUser, and ConductorUser.
- **Abstraction:** Uses interfaces such as PaymentStrategy to define common behavior.
- **Polymorphism:** Supports different user types and interchangeable payment implementations.

### Design Patterns Implemented

| Design Pattern | Implementation | Purpose |
|---|---|---|
| Factory | UserFactory, TicketFactory | Centralizes the creation of user and ticket objects. |
| Singleton | BookingManager | Provides a shared booking manager instance. |
| Strategy | PaymentStrategy | Supports interchangeable payment methods. |
| Builder | RouteBuilder, BusBuilder, ScheduleBuilder | Simplifies the construction of complex objects. |
| Repository | Spring Data JPA Repositories | Separates data access from business logic. |
| Dependency Injection | Spring Framework | Manages component dependencies and object creation. |

### Payment Strategy Implementation

The Strategy Pattern allows different payment methods to implement a common interface.

```text
              PaymentStrategy
                     |
          +----------+----------+
          |          |          |
          v          v          v
      CreditCard    UPI       Wallet
       Payment     Payment    Payment
          |          |          |
          +----------+----------+
                     |
               PaymentContext
```

New payment strategies can be introduced without changing the common payment interface.

---

## 🗄️ Database Design

The application uses Hibernate and Spring Data JPA for object-relational mapping and database persistence.

### Main Entities

| Entity | Responsibility |
|---|---|
| User | Stores user information and account roles. |
| Admin | Represents administrator accounts. |
| RegularUser | Represents passenger accounts. |
| DriverUser | Represents driver accounts. |
| ConductorUser | Represents conductor accounts. |
| Route | Stores source, destination, and distance. |
| Stop | Maintains route-related stop information. |
| Bus | Stores bus details and route associations. |
| Schedule | Stores travel dates, timings, and route associations. |
| Booking | Maintains passenger booking information and status. |
| Ticket | Stores ticket and fare information. |
| Transaction | Maintains payment transaction details and status. |

The User entity uses **Single Table Inheritance** to represent different user types within a common entity hierarchy.

### Database Configuration

The current application uses an H2 in-memory database for development and demonstration.

```properties
spring.datasource.url=jdbc:h2:mem:transportdb
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.hibernate.ddl-auto=update
spring.h2.console.enabled=true

server.port=8081
```

*Note: The database is in-memory, so stored application data is not retained after the application shuts down.*

---

## 💰 Fare Calculation Logic

The fare calculation service implements a distance-based pricing model.

- Base fare: ₹2 per kilometre.
- AC surcharge: 20% of base fare.
- Peak-hour surcharge: 10% of base fare.
- Tax: 18% of the subtotal.
- Refund calculation:
  - 50% refund when cancellation is less than 24 hours before departure.
  - 80% refund when cancellation is 24 hours or more before departure.

The fare service separates pricing calculations from controller logic.

---

## 📂 Project Structure

```text
public-transport-management-system/
│
├── .mvn/
│   └── wrapper/
│
├── src/
│   ├── main/
│   │   ├── java/com/transport/transport_system/
│   │   │   │
│   │   │   ├── controller/
│   │   │   │   ├── AdminController.java
│   │   │   │   ├── AuthController.java
│   │   │   │   ├── BookingController.java
│   │   │   │   ├── FareController.java
│   │   │   │   ├── RouteController.java
│   │   │   │   ├── ScheduleController.java
│   │   │   │   └── ...
│   │   │   │
│   │   │   ├── factory/
│   │   │   │   ├── UserFactory.java
│   │   │   │   └── TicketFactory.java
│   │   │   │
│   │   │   ├── model/
│   │   │   │   ├── User.java
│   │   │   │   ├── Admin.java
│   │   │   │   ├── RegularUser.java
│   │   │   │   ├── Route.java
│   │   │   │   ├── Schedule.java
│   │   │   │   ├── Bus.java
│   │   │   │   └── ...
│   │   │   │
│   │   │   ├── repository/
│   │   │   │   └── ...
│   │   │   │
│   │   │   ├── service/
│   │   │   │   ├── AuthService.java
│   │   │   │   ├── BookingService.java
│   │   │   │   ├── BookingManager.java
│   │   │   │   ├── RouteService.java
│   │   │   │   ├── ScheduleService.java
│   │   │   │   ├── FareService.java
│   │   │   │   └── PaymentService.java
│   │   │   │
│   │   │   ├── strategy/
│   │   │   │   ├── PaymentStrategy.java
│   │   │   │   ├── PaymentContext.java
│   │   │   │   ├── CreditCardPayment.java
│   │   │   │   ├── UPIPayment.java
│   │   │   │   └── WalletPayment.java
│   │   │   │
│   │   │   └── TransportSystemApplication.java
│   │   │
│   │   └── resources/
│   │       ├── templates/
│   │       └── application.properties
│   │
│   └── test/
│       └── java/com/transport/transport_system/
│           └── TransportSystemApplicationTests.java
│
├── .gitignore
├── .mvn/
├── mvnw
├── mvnw.cmd
├── pom.xml
├── README.md
│
├── IMPLEMENTATION_GUIDE.md
├── COMPLETE_IMPLEMENTATION_SUMMARY.md
├── USER_MANAGEMENT_DOCUMENTATION.md
├── UML_DIAGRAMS.md
└── UML_DIAGRAMS_NEW.md
```

---

## ⚙️ Installation & Setup

### Prerequisites

- Java Development Kit (JDK) 17 or compatible.
- Git.
- Internet connection for Maven dependency resolution.

### 1. Clone the Repository

```bash
git clone https://github.com/reddyvaishnavii/public-transport-management-system.git

cd public-transport-management-system
```

### 2. Run the Application

Using the included Maven Wrapper:

**macOS / Linux**

```bash
chmod +x mvnw
./mvnw spring-boot:run
```

**Windows**

```bash
mvnw.cmd spring-boot:run
```

Alternatively, if Maven is installed:

```bash
mvn spring-boot:run
```

### 3. Access the Application

Once the application starts successfully, open:

```text
http://localhost:8081
```

The H2 database console, when enabled, is available at:

```text
http://localhost:8081/h2-console
```

Use the JDBC URL configured in `application.properties` to connect.

---

## 🧪 Testing

The project includes the Spring Boot testing dependency and a basic application context loading test.

The current test suite is limited and does not yet provide comprehensive unit, integration, or end-to-end coverage.

Future testing improvements include:

- Unit tests for service-layer business logic.
- Repository tests for database operations.
- Controller tests for request handling.
- Booking and fare calculation test cases.
- Payment strategy tests.

---

## 📊 UML Documentation

The repository includes UML and implementation documentation covering:

- Use Case Diagrams.
- Class Diagrams.
- Activity Diagrams.
- State Diagrams.
- Payment and transaction workflows.
- User management and authentication workflows.

Refer to the following files for additional details:

- `UML_DIAGRAMS.md`
- `UML_DIAGRAMS_NEW.md`
- `IMPLEMENTATION_GUIDE.md`
- `USER_MANAGEMENT_DOCUMENTATION.md`
- `COMPLETE_IMPLEMENTATION_SUMMARY.md`

---

## 👥 Team Contributions

**Team of 4 — Object Oriented Analysis & Design Mini Project**

| Contributor | Major Responsibility | Additional Responsibility |
|---|---|---|
| Sindhu H | Multi-Role User Authentication | Profile Management & Booking History |
| Swathi D | Seat Reservation | Booking Cancellation & Refund |
| Sneha V | Fleet Management | Driver Assignment & Management |
| Vaishnavi Reddy | Route & Schedule Management | Fare Calculation |

**Vaishnavi Reddy's contribution:**

Focused on route and schedule management, including route information handling, schedule creation and retrieval, source-destination search, and fare calculation logic.

---

## 🎓 Course Information

- **Course:** UE23CS352B – Object Oriented Analysis & Design
- **Institution:** PES University
- **Project Type:** Team Mini Project
- **Team Size:** 4

---

## 🔮 Future Enhancements

- Integrate a production relational database such as MySQL or PostgreSQL.
- Implement secure password hashing and stronger authentication.
- Introduce transaction-safe seat allocation and concurrency handling.
- Integrate a real payment gateway.
- Add real-time GPS-based vehicle tracking.
- Improve automated unit and integration test coverage.
- Develop a mobile application.
- Explore AI-based route and schedule optimization.

---

## 📌 Project Status

An academic full-stack Java application demonstrating MVC architecture, object-oriented programming, database persistence, and software design patterns.

The project is currently intended for local development and educational demonstration. It has not been deployed to a production environment.

---

**Developed collaboratively by Sindhu H, Swathi D, Sneha V, and Vaishnavi R.**
