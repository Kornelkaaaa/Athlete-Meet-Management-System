# System Architecture

## Overview
Swimcloud is a role-based backend system designed to manage competitive swimming
data across athlete performance tracking, recruiting workflows, and meet
administration. The architecture prioritizes data integrity, clear separation
of concerns, and scalable workflow design.

This project focuses on backend system design rather than UI or deployment,
modeling how a real-world sports data platform would be structured.

---

## Architectural Style
The system follows a **layered architecture** inspired by MVC and domain-driven
design principles.

### API Layer
- Exposes REST-style endpoints for all system operations
- Handles request validation, authentication, and role-based authorization
- Acts as the entry point for all client interactions

### Service / Domain Layer
- Implements core business rules and workflows
- Coordinates multi-step operations such as recruiting actions and meet
  publishing
- Defines transactional boundaries to ensure atomic operations

### Data Access Layer
- Provides repository-based access to relational data
- Manages entity relationships and joins
- Enforces referential integrity through database constraints

---

## Role-Based Access Model
The system supports four primary roles, each with scoped permissions:

- **Swimmer**
  - View personal performance metrics and meet results
  - Manage profile and recruiting visibility

- **Coach**
  - View team and athlete performance
  - Refer swimmers and provide recruiting data

- **Recruiter**
  - Search and filter athletes
  - Manage recruiting lists and review referrals

- **Meet Administrator**
  - Create and manage meets and events
  - Generate heat sheets and publish official results

Authorization is enforced at the API and service layers to prevent unauthorized
access to sensitive data.

---

## Design Goals
- Maintain strong data consistency across complex workflows
- Support many-to-many relationships between athletes, events, and meets
- Enable analytics and historical performance tracking
- Separate recruiting data from athlete profiles to support multiple recruiters
- Ensure workflows fail safely using transaction rollback

---

## Documentation
Detailed data modeling and workflow behavior are documented in:
- `database-schema.md`
- `workflows.md`
- UML diagrams located in `/diagrams`
