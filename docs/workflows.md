# Backend Workflows

This document describes key backend workflows implemented at the service layer.
Each workflow is designed to be atomic, validated, and role-restricted.

---

## Add Swimmer to Recruiting List

**Actor:** Recruiter

1. Recruiter submits a search request with filters
2. System validates recruiter credentials and permissions
3. Swimmer performance data is retrieved
4. Recruiter selects a swimmer to recruit
5. A recruitment record is created linking recruiter and swimmer
6. Transaction commits or rolls back on failure

**Key Rules:**
- Recruiter must be authorized
- Duplicate recruitment records are prevented
- Swimmer visibility settings are enforced

---

## Refer Swimmer for Recruiting

**Actor:** Coach

1. Coach selects a swimmer from their team
2. Coach selects a recruiting institution
3. System validates coach affiliation and permissions
4. Referral data is stored and linked to the recruiter
5. Recruiter is notified of the referral

**Key Rules:**
- Coaches can only refer swimmers from their team
- Referral data is immutable once submitted

---

## Create Heat Sheet

**Actor:** Meet Administrator

1. Administrator selects a future meet
2. System validates meet state and admin permissions
3. Event entries and seed times are retrieved
4. Heat and lane assignments are generated
5. Heat sheet is saved and made available for review

**Key Rules:**
- Cannot generate heat sheets for completed meets
- Lane conflicts are automatically validated

---

## Publish Meet Results

**Actor:** Meet Administrator

1. Administrator selects a completed meet
2. System validates that all required results are present
3. Results are verified and approved
4. Meet results are published
5. Performance metrics are updated

**Key Rules:**
- Results cannot be modified after publishing
- Publishing triggers metric recalculation

---

## View Performance Metrics

**Actor:** Swimmer, Coach, Recruiter

1. User submits a metrics request with filters
2. System validates role-based access
3. Aggregated performance data is retrieved
4. Metrics are returned in a role-appropriate format

**Key Rules:**
- Recruiters only see permitted athlete data
- Metrics reflect the most recently published results

---

## Workflow Documentation
Detailed interaction sequences are documented in:
`/diagrams/sequence-diagrams.pdf`
