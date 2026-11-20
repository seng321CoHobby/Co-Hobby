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

This document specifies the functional, data and interface requirements of Co-Hobby's first release. It is written for the implementation team in Sprint 3 and later, for peer reviewers who must be able to implement the system from it, and for evaluators who check traceability from user story to API operation.

### 1.2 Scope

Co-Hobby helps people who struggle to find nearby partners for a hobby to create a hobbyist profile, find or form groups, fill open roles, track project progress, and share completed projects. The scope is identical to the Sprint 1 first-release scope (`docs/01-project-proposal.md`); this document refines it and does not expand it. `[CONFIRM against docs/01]`

- **Included:** hobbyist profile creation, group creation with open roles, group discovery, member assignment by the Project Owner, project initialization, sequential milestone progression, sharing completed projects to a public feed (US-01 to US-07).
- **Deferred:** selling services; becoming a general social media platform.

### 1.3 Definitions and Abbreviations

| Term | Definition |
|---|---|
| Hobbyist | Registered user with a hobbyist profile |
| Project Owner | Group creator; holds the OWNER member role |
| Milestone | Project stage: PLANNING → WEEK_1 → WEEK_2 → COMPLETED |
| Skill Role | A role a group needs filled, chosen from the predefined list (e.g. a position in the activity) |
| Open Role | A Skill Role in a group listing that has no member assigned yet |
| Public Feed | List of completed projects that were shared by their Project Owner |
| JWT | JSON Web Token sent as a Bearer token to authenticate API requests |

### 1.4 References

- Sprint 2 assignment text (Teams submission)
- `docs/01-project-proposal.md` — problem, stakeholders, scope
- `docs/02-vision-and-boundary.md` — vision, boundary, constraints
- `docs/05-product-backlog.md` — user stories and acceptance criteria
- `api/openapi.yaml` — API contract (source of truth for interfaces)
- Course slides: Requirements Engineering; OOAD & UML; Software Architecture

## 2. Overall Description

**User classes**

- **Solo Hobbyist:** a registered user looking for a group for a hobby. Can create a profile, search groups and view the public feed.
- **Project Owner:** a Hobbyist who created a group. Additionally can assign members, create the project, advance milestones and share the completed project.
- **API clients:** the client applications that call the API (e.g. the web frontend). `[CONFIRM against docs/02]`

**Operating environment:** the system is a web API described by `api/openapi.yaml`, served over HTTP locally and HTTPS when deployed.

**Constraints** (from `docs/02`)

- Authenticated requests use a Bearer JWT.
- Mutations on a group or project are restricted to its OWNER.
- Project stages advance sequentially only (PLANNING → WEEK_1 → WEEK_2 → COMPLETED).
- No feature beyond US-01 to US-07.

**Assumptions and risks** (from `docs/01`)

- Users create one profile each and use real information.
- Risk: fake self-created accounts could be used to boost the visibility of a group or project.
- Risk: the platform could be used to promote paid services, which is outside the first-release scope.

`[CONFIRM wording against docs/01 and docs/02]`

## 3. Functional Requirements

Each requirement maps to exactly one user story. No scope is added beyond the seven stories. Acceptance criteria below are written from the API contract; align their wording with `docs/05-product-backlog.md`. `[CONFIRM]`

### 3.1 Epic 1 — Hobbyist Identity

| ID | Requirement | User Story | Acceptance Criteria |
|---|---|---|---|
| FR-1.1 | The system shall provide predefined hobby categories and skill roles. | US-01 | `GET /tags` returns the list of categories and roles with 200. |
| FR-1.2 | The system shall allow a registered user to create a hobbyist profile. | US-01 | A valid request creates the profile and returns 201; an invalid body returns 400; a missing or invalid token returns 401. |

### 3.2 Epic 2 — Group Formation

| ID | Requirement | User Story | Acceptance Criteria |
|---|---|---|---|
| FR-2.1 | The system shall allow a creator to create a group with open roles. | US-02 | A valid request with at least one needed role returns 201 and the creator becomes OWNER; an empty role list returns 400; no token returns 401. |
| FR-2.2 | The system shall allow searching groups by category and role. | US-03 | `GET /groups` with a category and/or role filter returns matching groups that still have open roles with 200; an invalid filter returns 400. |
| FR-2.3 | The system shall allow the Project Owner to assign a member to an open role. | US-04 | The OWNER can fill an open role and receives 200; a non-owner gets 403; a filled role or duplicate member gets 409. |

### 3.3 Epic 3 — Project Execution and Showcase

| ID | Requirement | User Story | Acceptance Criteria |
|---|---|---|---|
| FR-3.1 | The system shall allow the Project Owner to initialize a project in PLANNING. | US-05 | The OWNER of an existing group creates a project in stage PLANNING and receives 201; a non-owner gets 403; an unknown group gets 404. |
| FR-3.2 | The system shall allow sequential milestone advancement only. | US-06 | The OWNER can move a project to the next stage only and receives 200; skipping or repeating a stage returns 409; a non-owner gets 403. |
| FR-3.3 | The system shall allow sharing completed projects to a public feed. | US-07 | The OWNER can share a COMPLETED project and receives 200; sharing a project that is not completed or already shared returns 409; the feed is readable without login via `GET /feed/projects`. `[CONFIRM login rule]` |

## 4. Use Cases

> House style: actor, preconditions, main flow, alternate/error flows, postconditions.
> UC-04 is written out fully as the example to copy for the others.

### UC-01 Create Profile (US-01)

- **Primary actor:** Hobbyist (registered user)
- **Preconditions:**
  - User has a valid Bearer JWT.
  - User does not yet have a hobbyist profile. `[CONFIRM]`
- **Main flow:**
  1. User requests the predefined hobby categories and skill roles.
  2. System returns the list.
  3. User submits a profile with selected categories and skill roles.
  4. System authenticates the token.
  5. System validates the request body.
  6. System stores the profile.
  7. System returns 201 with the created profile.
- **Alternate/error flows:**
  - E1: Missing or invalid authentication → 401.
  - E2: Invalid or incomplete body (e.g. unknown category, missing required field) → 400.
- **Postconditions:** A hobbyist profile exists for the user.

### UC-02 Create Group (US-02)

- **Primary actor:** Hobbyist (becomes Project Owner)
- **Preconditions:**
  - User has a valid Bearer JWT.
  - User has a hobbyist profile. `[CONFIRM]`
- **Main flow:**
  1. User submits a group listing with title, hobby category and the list of needed skill roles.
  2. System authenticates the token.
  3. System validates the body, including at least one needed role.
  4. System creates the group and assigns the user the OWNER member role.
  5. System returns 201 with the group listing.
- **Alternate/error flows:**
  - E1: Missing or invalid authentication → 401.
  - E2: Invalid body, such as an empty needed-role list or unknown category → 400.
- **Postconditions:** A group with open roles exists and the creator is its OWNER.

### UC-03 Discover Groups (US-03)

- **Primary actor:** Hobbyist
- **Preconditions:** Groups may exist; no login restriction is specified for browsing. `[CONFIRM against openapi security]`
- **Main flow:**
  1. User selects a hobby category and/or skill role filter.
  2. System validates the filter.
  3. System returns the groups that match and still have open roles.
  4. User views a group listing and its open roles.
- **Alternate/error flows:**
  - E1: Invalid filter value → 400.
  - A1: No group matches → system returns 200 with an empty list.
- **Postconditions:** None; no data is changed.

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

- **Primary actor:** Project Owner
- **Secondary actor:** Hobbyist (reads the public feed)
- **Preconditions:**
  - Owner has a valid Bearer JWT.
  - The group exists and the requester is its OWNER.
- **Main flow:**
  1. Owner creates a project for the group; the system creates it in stage PLANNING and returns 201 (US-05).
  2. Owner advances the project to WEEK_1; the system validates the order and returns 200 (US-06).
  3. Owner advances the project to WEEK_2; the system returns 200.
  4. Owner advances the project to COMPLETED; the system returns 200.
  5. Owner shares the completed project; the system publishes it and returns 200 (US-07).
  6. Any user can see the project in the public feed (`getSharedProjectsFeed`).
- **Alternate/error flows:**
  - E1: Missing or invalid authentication → 401.
  - E2: Requester is not OWNER → 403.
  - E3: Unknown group or project → 404.
  - E4: Invalid body (e.g. unknown stage value) → 400 on create and progress operations.
  - E5: Stage skipped or repeated → 409 on `updateProjectProgress`.
  - E6: Project not yet COMPLETED, or already shared → 409 on `shareProject`. `[CONFIRM exact condition in openapi]`
- **Postconditions:** The project is in its new stage; after step 5 it appears in the public feed.

## 5. Data Requirements

Every entity below must match the `api/openapi.yaml` component schemas exactly. Field-level details marked `[CONFIRM]` need a final check against the contract.

| Entity (schema) | Purpose | Field rules |
|---|---|---|
| TagCategory | Predefined hobby category with its skill roles | Read-only list returned by `getTags`. `[CONFIRM fields]` |
| NewProfile / ProfileResponse | Hobbyist profile request and response | Identifier is a UUID in the response; selected categories and roles must exist in TagCategory. `[CONFIRM required fields]` |
| NewGroupListing / GroupListingResponse | Group creation request and group listing response | Identifier is a UUID; `neededRoles` is an array with `minItems` 1; optional media URLs use URI format. |
| GroupMember | Member of a group | `memberRole` enum OWNER / MEMBER, which is distinct from `skillRole`. |
| AddMemberRequest | Request to assign a member | Contains the user's UUID and the `skillRole` to fill; both required. |
| NewProject / ProjectResponse | Project request and response | Identifier is a UUID; new projects start in PLANNING; `stage` enum PLANNING, WEEK_1, WEEK_2, COMPLETED. |
| ProgressUpdateRequest | Request to advance a stage | `stage` enum; only the next stage is accepted. |
| Problem | Error response body | Returned for 4xx errors; carries a machine-readable code such as ROLE_SLOT_FULL. `[CONFIRM fields]` |

**General field rules:** identifiers are UUIDs, media URLs use URI format, required fields are enforced by the schema, and `neededRoles` must contain at least one role.

## 6. Interface Requirements

Every endpoint is listed with its operationId and its representative success and error responses. The contract in `api/openapi.yaml` is authoritative.

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

**Representative responses**

- **Success:** the created or updated resource (profile, group listing, project) as the matching `*Response` schema.
- **Error:** a `Problem` object with the HTTP status. Example: adding a member to a filled role returns 409 with code ROLE_SLOT_FULL.

## 7. Non-Functional Requirements

See `docs/07-nfr-quality-measures.md`.

## 8. Requirements Traceability Matrix

> The API-operation column is pre-filled from `api/openapi.yaml` (contract source of truth).
> FR and UC references match sections 3 and 4.

| FR | User Story | Use Case | API Operation(s) |
|---|---|---|---|
| FR-1.1, FR-1.2 | US-01 | UC-01 | getTags, createProfile |
| FR-2.1 | US-02 | UC-02 | createGroup |
| FR-2.2 | US-03 | UC-03 | listAvailableGroups |
| FR-2.3 | US-04 | UC-04 | addGroupMember |
| FR-3.1 | US-05 | UC-05 | createProject |
| FR-3.2 | US-06 | UC-05 | updateProjectProgress |
| FR-3.3 | US-07 | UC-05 | shareProject, getSharedProjectsFeed |
