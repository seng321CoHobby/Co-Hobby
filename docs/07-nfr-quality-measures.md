# Non-Functional Requirements and Quality-Measure Specifications

**Course:** SENG 321 Software Engineering
**Team:** 19
**Project:** Co-Hobby
**Sprint:** 2
**Status:** NFR Catalogue authored by @yigitozkaya07 (Issue #28); verification-tooling section pending @sengProje64 (Issue #29)

> Define quality in terms of *measurable criteria and verification methods*, not claims.
> The system is not yet implemented: numeric values are **validation targets** for later
> sprints (Sprint 3–4), never assertions the current team must prove now. Avoid bare SLAs
> with no measurement plan.
> This document must exist **before** `docs/08-architecture.md` is finalized (NFRs drive the
> C4 design decisions).

## 1. Purpose

This document defines the measurable non-functional requirements (NFRs) and quality-verification plans for the first release of **Co-Hobby** (Spring Boot REST backend, web frontend, and OpenAPI 3.1.0 contract). Because the first release focuses on dependable partner discovery, role-based group formation, sequential milestone tracking, and public project sharing—while deferring chat, swipe matching, payments, notifications, and raw media hosting—explicit quality attributes are required to guide architectural decisions in `docs/08-architecture.md` (`ARCH-01`) and test planning in Issue `#29` (`NFR-02`).

Every requirement below specifies a **validation target** to be evaluated during implementation sprints (Sprint 3–4) using a concrete automated or moderated verification method rather than claiming unverified runtime SLAs in Sprint 2.

## 2. NFR Catalogue

> Fill one row per NFR. Every row needs a measurable criterion **and** a verification method.

### 2.1 Performance

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-P-01 | API endpoints respond within a bounded latency under expected load. | **Validation target:** p95 response time **< 300 ms** for public read endpoints (`GET /tags`, `GET /groups`, `GET /feed/projects`) and **< 500 ms** for authenticated write endpoints (`POST`/`PATCH`) under a simulated class-scale load of **50 concurrent virtual users** with **< 1%** HTTP 5xx error rate. | JMeter (or k6) load test against the deployed Spring Boot API | Sprint 4 |
| NFR-P-02 | Public feed and group search views load without blocking user interaction. | **Validation target:** Largest Contentful Paint (LCP) **<= 2.5 s** and First Input Delay / Interaction to Next Paint (INP) **<= 200 ms** on the group search and public shared-projects feed pages using sample portfolio URLs. | Chrome DevTools browser timing trace and Lighthouse Performance audit against the deployed web app | Sprint 4 |

### 2.2 Security

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-S-01 | All write operations require a valid Bearer JWT (`BearerAuth`), while public read endpoints remain accessible without authentication. | **Validation target:** **100%** of write endpoints (`POST /profiles`, `POST /groups`, `POST /groups/{groupId}/members`, `POST /projects`, `PATCH /projects/{projectId}/progress`, `POST /projects/{projectId}/share`) reject missing, malformed, or expired Bearer JWT tokens with HTTP `401 Unauthorized`; `GET /tags`, `GET /groups`, and `GET /feed/projects` succeed without a token (`security: []`). | Automated API integration tests (`401` and unauthenticated `200` cases) using JUnit 5 / MockMvc matching `api/openapi.yaml` | Sprint 3 |
| NFR-S-02 | `OWNER`-restricted mutations reject non-owners (`MEMBER` or unrelated authenticated users). | **Validation target:** **100%** of restricted operations (`POST /groups/{groupId}/members`, `POST /projects`, `PATCH /projects/{projectId}/progress`, `POST /projects/{projectId}/share`) return HTTP `403 Forbidden` when invoked by any authenticated user who is not the group's `OWNER`. | Automated role-matrix API integration tests (`403` cases) verifying `OWNER` vs. `MEMBER` enforcement | Sprint 3 |
| NFR-S-03 | External media references are bounded and validated without hosting raw media files. | **Validation target:** **100%** of `mediaUrls` entries in `POST /profiles` satisfy the OpenAPI `format: uri` schema and enforce well-formed `http`/`https` schemes as an implementation-level validation rule; invalid URI formats, disallowed schemes, or missing required fields return HTTP `400 Bad Request` (`application/problem+json`). | Automated API contract and Bean Validation tests on `NewProfile.mediaUrls` | Sprint 3 |
| NFR-S-04 | Transport security and data minimization protect deployed traffic and user records. | **Validation target:** **HTTPS (TLS 1.2+)** enforced on deployed environments; **0** financial/payment or medical fields present in API schemas or database entities; **0** hardcoded secrets committed to the repository. | Deployment checklist, schema review against `api/openapi.yaml`, and GitHub secret scanning | Sprint 3 / Sprint 4 |

### 2.3 Usability

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-U-01 | A new hobbyist can create a profile and find a compatible group quickly. | **Validation target:** Group discovery (filtering open groups by `category` and `seekingRole` and reaching a compatible group match) completes in **under three minutes** with **>= 90%** task completion rate in a moderated usability test (from the Sprint 1 proposal). | Moderated usability test with at least 5 evaluators on the Figma prototype and later the web app; record task completion time and success rate | Sprint 3 / Sprint 4 |
| NFR-U-02 | Users understand group vacancies and required skill roles without asking the owner. | **Validation target:** **>= 90%** of usability test participants correctly identify a group's category, creator role, and open `neededRoles` on the first attempt without facilitator hints. | Moderated usability test scenario with post-task comprehension questions and first-attempt success rate metric | Sprint 4 |

### 2.4 Reliability

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-R-01 | Domain rules never allow invalid state (duplicate members, filled vacancies, skipped/backward stages, or sharing unfinished projects). | **Validation target:** **100%** of `409`-path cases—duplicate member addition, assigning an already-filled role (`ROLE_SLOT_FULL`), skipping or reversing `PLANNING -> WEEK_1 -> WEEK_2 -> COMPLETED`, or calling `/share` before `COMPLETED`—return HTTP `409 Conflict` and persist **0** inconsistent state changes. | Transactional API integration tests (`409` cases) and state-machine unit tests in JUnit 5 | Sprint 3 |
| NFR-R-02 | Error responses and missing-resource handling remain predictable and resilient when external auth is unavailable locally. | **Validation target:** **100%** of `400` and `409` error responses conform to the `Problem` schema (`application/problem+json`: `title`, `status`, `code`, `detail`); unknown group/user/project UUIDs return HTTP `404 Not Found`; local development and CI tests pass deterministically using the documented local JWT stub. | Automated API contract assertions (`400`/`404`/`409` cases) and CI test execution against the local JWT stub | Sprint 3 |

### 2.5 Maintainability

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-M-01 | API contract remains valid and consistent with implementation. | **Validation target:** OpenAPI 3.1.0 lint passes with **0 errors** on every pull request that changes \api/openapi.yaml``. | Existing Redocly workflow `.github/workflows/validate-openapi.yml` | Sprint 2 → 4 |
| NFR-M-02 | Codebase stays testable, modular, and reviewable across team members. | **Validation target:** **>= 70%** unit/integration line coverage on core backend domain and service classes; **0** critical static-analysis/lint errors; **100%** of PRs to `develop` pass CI checks, reference an issue (`Refs #N`), and receive at least 1 peer approval. | CI coverage report (JaCoCo), static-analysis/lint workflow (Checkstyle/SpotBugs), and GitHub branch rulesets | Sprint 3 |

### 2.6 Accessibility

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-A-01 | UI is accessible to common assistive technologies and users with visual impairments. | **Validation target:** Lighthouse Accessibility score **>= 90** with **0** critical/serious **WCAG 2.1 Level AA** violations (including **>= 4.5:1** text contrast ratio, semantic headings, and explicit `<label>` / ARIA labels on all form inputs). | Lighthouse accessibility audit and axe DevTools check on the Figma contrast review and deployed web app | Sprint 4 |
| NFR-A-02 | Core discovery and project-tracking flows are operable without a mouse. | **Validation target:** **100%** of primary interactive controls (profile form, category/role search filters, member assignment, milestone update, and project share buttons) are reachable and operable via keyboard (`Tab`, `Shift+Tab`, `Enter`, `Space`) with visible focus indicators. | Manual keyboard-only navigation checklist executed across `US-01` through `US-07` screens | Sprint 4 |

## 3. Quality Verification Tooling and Test Plans (Issue #29 — DevOps)

<TODO: @sengProje64 fills this section after the NFR catalogue is stable. For each NFR above,
name the concrete tool and the CI step that verifies it.>

- **Existing CI:** `.github/workflows/validate-openapi.yml` — contract lint on every PR (keep it green).
- **Planned Sprint 3 CI changes:** build + test workflow, coverage threshold, contract checks.
- **Demo-day load-test scenario:** <TODO: class-scale concurrent-user event for the performance NFRs>.
- **PR quality gates (later sprints):** CI passing, contract valid, review approved, no failing required checks.

## 4. Quality Measurement Rules

1. Every NFR names a criterion and a verification method; no exceptions.
2. Unverified numbers are labeled **validation targets**, never reported as achieved.
3. A quality claim is only "met" when the verification method has actually run and its evidence is linked here.
4. Quality claims must not contradict `api/openapi.yaml` or the Sprint 1 boundary.
