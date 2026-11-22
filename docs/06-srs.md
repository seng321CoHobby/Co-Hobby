# Software Requirements Specification (SRS)

**Course:** SENG 321 Software Engineering
**Team:** 19
**Project:** Co-Hobby
**Sprint:** 2
**Status:** Draft — skeleton prepared by @Bruhun, authored by @beyazitKRGL (Issue #26)

> This document expands the Sprint 1 project proposal, system boundary, and initial backlog
> into a detailed SRS. It must not introduce features beyond the Sprint 1 first-release scope
> (US-01 through US-07). Follow the structure of the lecturer's Sprint 1 examples pack and the
> requirements-engineering slide notation.

## 1. Introduction

### 1.1 Purpose

<TODO: what this document is for and who reads it (implementation team in Sprint 3+, peer reviewers, evaluators).>

### 1.2 Scope

<TODO: restate the first-release scope from `docs/01-project-proposal.md` (included vs deferred).
Must remain identical to the Sprint 1 scope — refinement, not expansion.>

### 1.3 Definitions and Abbreviations

| Term | Definition |
|---|---|
| Hobbyist | Registered user with a hobbyist profile |
| Project Owner | Group creator; holds the OWNER member role |
| Milestone | Project stage: PLANNING → WEEK_1 → WEEK_2 → COMPLETED |
| <TODO> | <TODO> |

### 1.4 References

- Sprint 2 assignment text (Teams submission)
- `docs/01-project-proposal.md` — problem, stakeholders, scope
- `docs/02-vision-and-boundary.md` — vision, boundary, constraints
- `docs/05-product-backlog.md` — user stories and acceptance criteria
- `api/openapi.yaml` — API contract (source of truth for interfaces)
- Course slides: Requirements Engineering; OOAD & UML; Software Architecture

## 2. Overall Description

<TODO: user classes (Solo Hobbyist, Project Owner, external systems), operating environment,
constraints (HTTP-local / HTTPS-deployed, JWT Bearer, OWNER-restricted mutations,
sequential stages) reusing docs/02, and the assumptions/risks from docs/01.>

## 3. Functional Requirements

<TODO: functional requirements per epic. One row per requirement; each maps to exactly one
user story. Do not add scope beyond the seven stories.>

### 3.1 Epic 1 — Hobbyist Identity

| ID | Requirement | User Story | Acceptance Criteria |
|---|---|---|---|
| FR-1.1 | The system shall provide predefined hobby categories and skill roles. | US-01 | <TODO> |
| FR-1.2 | The system shall allow a registered user to create a hobbyist profile. | US-01 | <TODO> |

### 3.2 Epic 2 — Group Formation

| ID | Requirement | User Story | Acceptance Criteria |
|---|---|---|---|
| FR-2.1 | The system shall allow a creator to create a group with open roles. | US-02 | <TODO> |
| FR-2.2 | The system shall allow searching groups by category and role. | US-03 | <TODO> |
| FR-2.3 | The system shall allow the Project Owner to assign a member to an open role. | US-04 | <TODO> |

### 3.3 Epic 3 — Project Execution and Showcase

| ID | Requirement | User Story | Acceptance Criteria |
|---|---|---|---|
| FR-3.1 | The system shall allow the Project Owner to initialize a project in PLANNING. | US-05 | <TODO> |
| FR-3.2 | The system shall allow sequential milestone advancement only. | US-06 | <TODO> |
| FR-3.3 | The system shall allow sharing completed projects to a public feed. | US-07 | <TODO> |

## 4. Use Cases

> House style: actor, preconditions, main flow, alternate/error flows, postconditions.
> UC-04 is written out fully as the example to copy for the others.

### UC-01 Create Profile (US-01)

<TODO>

### UC-02 Create Group (US-02)

<TODO>

### UC-03 Discover Groups (US-03)

<TODO>

### UC-04 Assign Member to an Open Role (US-04) — EXAMPLE

- **Primary actor:** Project Owner
- **Secondary actor:** Hobbyist (member being added)
- **Preconditions:**
  - Owner has a valid Bearer JWT.
  - Target group exists.
  - The requested skill role still has an open vacancy.
- **Main flow:**
  1. Owner submits userId and skillRole for the group.
  2. System authenticates the token.
  3. System verifies the requester is the group's OWNER.
  4. System verifies the group exists and the role is still open.
  5. System adds the user as MEMBER with the requested skillRole.
  6. System returns 200 with the updated group listing.
- **Alternate/error flows:**
  - E1: Missing or invalid authentication → 401.
  - E2: Requester is not OWNER → 403.
  - E3: Unknown group or user ID → 404.
  - E4: Duplicate member or role already filled → 409 (ROLE_SLOT_FULL).
- **Postconditions:** Role vacancy is filled; group contains the new MEMBER.

### UC-05 Advance Milestones and Share Project (US-05, US-06, US-07)

<TODO: main success flow for PLANNING → WEEK_1 → WEEK_2 → COMPLETED → share.>

## 5. Data Requirements

<TODO: describe each entity and field rule. Cross-check against `api/openapi.yaml`
component schemas; every entity here must match the contract exactly.>

- TagCategory, NewProfile / ProfileResponse, NewGroupListing / GroupListingResponse,
  GroupMember (memberRole enum OWNER/MEMBER distinct from skillRole), AddMemberRequest,
  NewProject / ProjectResponse, ProgressUpdateRequest (stage enum), Problem
- Field rules: UUID identifiers, URI format for media URLs, required fields, minItems for neededRoles.

## 6. Interface Requirements

<TODO: map every endpoint to its operationId and representative success/error responses.>

| Path | OperationId | Method | Success | Errors |
|---|---|---|---|---|
| `/tags` | getTags | GET | 200 | 400 |
| `/profiles` | createProfile | POST | 201 | 400, 401 |
| `/groups` | listAvailableGroups | GET | 200 | 400 |
| `/groups` | createGroup | POST | 201 | 400, 401 |
| `/groups/{groupId}/members` | addGroupMember | POST | 200 | 400, 401, 403, 404, 409 |
| `/projects` | createProject | POST | 201 | 400, 401, 403, 404 |
| `/projects/{projectId}/progress` | updateProjectProgress | PATCH | 200 | 400, 401, 403, 404, 409 |
| `/projects/{projectId}/share` | shareProject | POST | 200 | 401, 403, 404, 409 |
| `/feed/projects` | getSharedProjectsFeed | GET | 200 | 400 |

## 7. Non-Functional Requirements

See `docs/07-nfr-quality-measures.md`.

## 8. Requirements Traceability Matrix

> The API-operation column is pre-filled from `api/openapi.yaml` (contract source of truth).
> Fill FR and UC references once the sections above are complete.

| FR | User Story | Use Case | API Operation(s) |
|---|---|---|---|
| FR-1.1, FR-1.2 | US-01 | UC-01 | getTags, createProfile |
| FR-2.1 | US-02 | UC-02 | createGroup |
| FR-2.2 | US-03 | UC-03 | listAvailableGroups |
| FR-2.3 | US-04 | UC-04 | addGroupMember |
| FR-3.1 | US-05 | UC-05 | createProject |
| FR-3.2 | US-06 | UC-05 | updateProjectProgress |
| FR-3.3 | US-07 | UC-05 | shareProject, getSharedProjectsFeed |

## 9. UML Models

The use cases in §4 and the milestone rules in FR-3.2 and FR-3.3 are modelled in UML:

- Use-case diagram ([`diagrams/uml-use-case.md`](diagrams/uml-use-case.md), PNG [`diagrams/uml-use-case.png`](diagrams/uml-use-case.png)): every use case is tagged with its user story and its UC-01 to UC-05 identifier.
- Project milestone state diagram ([`diagrams/uml-state.md`](diagrams/uml-state.md), PNG [`diagrams/uml-state.png`](diagrams/uml-state.png)): the states and 409 conflict transitions behind UC-05, FR-3.2 and FR-3.3.
