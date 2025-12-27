# Swimcloud Backend – Athlete & Meet Management System

## Overview
**Swimcloud Backend** is a role-based backend system designed to manage competitive swimming data, including athlete performance metrics, recruiting workflows, and meet operations. The project focuses on backend architecture, relational database modeling, API design, and transactional workflows for a multi-actor domain involving swimmers, coaches, recruiters, and meet administrators.

This repository represents an academic backend system design project, emphasizing scalability, data integrity, and domain-driven modeling rather than a production deployment.

---

## Backend Architecture
The system follows a layered backend architecture with clear separation of concerns:

### API Layer
- Exposes REST-style endpoints for system operations  
- Handles request validation, authentication, and role-based authorization  
- Enforces input constraints before invoking business logic  

### Service / Domain Layer
- Implements business rules for recruiting, meet management, and analytics  
- Coordinates multi-step workflows (e.g., heat sheet generation, recruiting actions)  
- Defines transactional boundaries and failure handling  

### Data Access Layer
- Repository-based access to relational entities  
- Manages persistence, joins, and historical data retrieval  
- Enforces referential integrity through primary and foreign key constraints  

---

## Domain Model & Database Design
The backend is built around a normalized relational schema that mirrors real-world swim operations.

### Core Domain Entities
- Swimmer – athlete profiles, demographics, visibility controls  
- Coach – team management and recruiting support  
- Recruiter – athlete evaluation and recruiting workflows  
- MeetAdmin – event and result management  
- Meet – competition metadata and lifecycle state  
- Event – distance, stroke, and scheduling  
- Team – organizational structure  
- Recruitment – recruiter–athlete relationships  

### Associative Tables
- EventSwimmer – many-to-many athlete participation  
- HeatRelatedSwimmer – heat and lane assignments  
- Attendance and participation tracking tables  

### Design Highlights
- Referential integrity enforced via foreign keys  
- Support for many-to-many relationships without data duplication  
- Historical performance retention for analytics and recruiting  
- Decoupled recruitment data allowing multiple recruiters per athlete  

---

## API Design (Conceptual)
The backend defines REST-style service boundaries aligned with domain workflows.

### Authentication & Authorization
- POST /auth/login  
- GET /auth/me  

### Athlete & Performance Services
- GET /swimmers/{id}  
- GET /swimmers/{id}/metrics  
- GET /meets/{id}/results  

### Recruiting Services
- GET /recruiting/swimmers  
- POST /recruiting/{swimmerId}/refer  
- POST /recruiting/{swimmerId}/add  
- GET /recruiting/lists  

### Meet Management Services
- POST /meets  
- POST /meets/{id}/heats  
- PUT /meets/{id}/heats  
- POST /meets/{id}/results  

*Endpoints are conceptual and demonstrate API boundaries rather than a deployed implementation.*

---

## Transaction Management & Validation
The backend enforces strong transactional guarantees:
- Atomic operations for recruiting updates and meet result publishing  
- Automatic rollback on validation or authorization failure  
- Validation rules include:
  - Duplicate lane assignment detection  
  - Meet state enforcement (future, active, completed)  
  - Required performance and event data checks  

---

## Analytics & Data Processing
Backend services support:
- Aggregation of athlete performance across meets and seasons  
- Improvement and consistency calculations  
- Recruiting benchmarks aligned with collegiate standards  
- Role-based query filtering to control data exposure  

Queries are optimized for time-based filtering, event-level comparisons, and recruiter-driven athlete discovery.

---

## Security & Access Control
- Role-based authorization enforced at API and service layers  
- Swimmer-controlled visibility for recruiting data  
- Restricted access to sensitive performance and recruiting information  
- Audit-style logging for profile, recruiting, and result updates  

---

## UML & System Documentation
This repository includes:
- Class diagrams for domain modeling and database schema  
- Sequence diagrams illustrating backend workflows and API interactions  
- Use case diagrams mapping business requirements to backend services  

---

## Backend Concepts Demonstrated
- Relational database design (PK/FK constraints, associative tables)  
- RESTful API design (conceptual)  
- Transaction management and rollback strategies  
- Role-based access control  
- Domain-driven modeling and layered architecture  

---

## Disclaimer
This project represents a backend system design and modeling exercise created for academic purposes. It is not a production-ready deployment but demonstrates backend architectural reasoning and data-driven design.
