# Database Schema Overview

## Design Approach
The Swimcloud backend uses a **normalized relational database schema** designed
to accurately model real-world swim competitions, recruiting relationships, and
performance tracking.

The schema emphasizes:
- Referential integrity
- Clear ownership of data
- Support for historical analytics
- Efficient querying for performance and recruiting workflows

---

## Core Entities

### Swimmer
Stores athlete profile and demographic information.
- Primary identifier for performance and recruiting data
- Linked to teams, events, and meets
- Visibility settings control recruiter access

### Coach
Represents team-affiliated coaches.
- Associated with one or more teams
- Can provide recruiting data and referrals for swimmers

### Recruiter
Represents college or university recruiters.
- Linked to recruiting institutions
- Maintains recruiting lists and athlete evaluations

### MeetAdmin
Manages official meet operations.
- Controls meet creation, heat sheets, and result publishing

### Team
Represents a swim team or school.
- Links swimmers and coaches
- Used for team-level performance analytics

---

## Meet & Event Entities

### Meet
Stores competition-level data.
- Includes date range, capacity, and status
- Acts as a parent entity for events and heat sheets

### Event
Represents individual swim events within a meet.
- Defined by distance, stroke, and scheduled time
- Linked to participating swimmers

### HeatSheet
Associates swimmers with specific heats and lanes.
- Generated and edited by meet administrators
- Used as the basis for official meet results

---

## Recruitment Entity

### Recruitment
Acts as an associative entity between swimmers and recruiters.
- Supports many-to-many recruiter–athlete relationships
- Stores recruiting status, dates, and evaluation metrics
- Decouples recruiting data from swimmer profiles

---

## Associative Tables
To support complex relationships, the schema includes:
- **EventSwimmer** – links swimmers to events (many-to-many)
- **HeatRelatedSwimmer** – links swimmers to heat assignments
- **Attendance tables** – track swimmer and coach participation at meets

---

## Integrity & Constraints
- Primary and foreign keys enforce referential integrity
- Cascade rules prevent orphaned records
- Composite keys are used where appropriate for associative tables
- Validation rules ensure consistent event, meet, and recruitment data

---

## Schema Documentation
The complete relational model is illustrated in:
`/diagrams/class-diagram.pdf`
