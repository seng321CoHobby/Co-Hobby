# Non-Functional Requirements and Quality-Measure Specifications

**Course:** SENG 321 Software Engineering
**Team:** 19
**Project:** Co-Hobby
**Sprint:** 2
**Status:** NFR Catalogue authored by @yigitozkaya07 (Issue #28); verification-tooling section (Section 3) authored by @sengProje64 (Issue #29)

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

This section turns the NFR catalogue into concrete tools, CI steps, and test events. Everything
here is a **plan for Sprint 3–4**: only the OpenAPI lint workflow exists today. A measure counts
as "met" only after the listed tool has run and its evidence (CI run link, report artifact) is
linked here (rule 3 in Section 4).

### 3.1 Verification Tool per NFR

| NFR | Verification tool | Where it runs | Evidence produced | Becomes active |
|---|---|---|---|---|
| NFR-P-01 | **k6** load script (`perf/api-load.js`) against the deployed API; JMeter accepted as an alternative | Manual workflow (`workflow_dispatch`) + demo-day load test (3.3) | k6 summary (p95 latency, error rate) uploaded as a workflow artifact | Sprint 4 |
| NFR-P-02 | **Lighthouse CI** (`@lhci/cli`) performance category on the feed page | `frontend.yml` on PRs touching the frontend | Lighthouse report (LCP, INP/TBT, performance score) as artifact | Sprint 4 |
| NFR-S-01 | **JUnit 5 + Spring Boot Test (MockMvc)** integration tests: every write endpoint called without/with an invalid JWT must return 401 | `ci.yml` → `mvn verify` | Surefire/Failsafe test report | Sprint 3 |
| NFR-S-02 | JUnit 5 + MockMvc: every OWNER-only operation called by a non-owner must return 403 | `ci.yml` → `mvn verify` | Test report | Sprint 3 |
| NFR-S-03 | Contract tests on the `mediaUrls` schema (invalid URI → 400) plus **Schemathesis** run against the running API | `ci.yml` → `contract` job | Schemathesis report, test report | Sprint 3 |
| NFR-S-04 | **GitHub secret scanning** (with push protection) on the repository; schema review of `api/openapi.yaml` and database entities for payment/medical fields; deployment checklist confirming HTTPS (TLS 1.2+) | Repository settings (continuous) + PR review + manual pre-deployment check | Secret-scanning alert list (0 open alerts), completed schema-review and deployment checklists | Sprint 3 / 4 |
| NFR-U-01 | Moderated usability test (prototype in Sprint 3, web app in Sprint 4) with a recorded task-time sheet | Manual, organized by QA | Task time and success-rate table linked from this document | Sprint 3 / 4 |
| NFR-U-02 | Usability test scenario "find a group that needs my role" | Manual, organized by QA | Success-rate table | Sprint 4 |
| NFR-R-01 | JUnit 5 + **Testcontainers (PostgreSQL)** integration tests for every 409 path (duplicate member, filled vacancy, skipped stage, share before `COMPLETED`), including a concurrent-request test for the same vacancy | `ci.yml` → `mvn verify` | Test report | Sprint 3 |
| NFR-R-02 | JUnit 5 + MockMvc contract assertions that every 400/409 response matches the `Problem` schema (`application/problem+json`) and unknown UUIDs return 404; all CI tests run against the local JWT stub | `ci.yml` → `mvn verify` and `contract` job | Test report, Schemathesis report | Sprint 3 |
| NFR-M-01 | **Redocly CLI** lint of `api/openapi.yaml` (existing `validate-openapi.yml`) | Every PR touching `api/openapi.yaml` | Workflow check status | Active now |
| NFR-M-02 | **JaCoCo** coverage report with a minimum-coverage rule; **Checkstyle** (Google style) and **SpotBugs** for the backend; ESLint for the frontend; GitHub branch rulesets for issue reference and approval | `ci.yml` / `frontend.yml` | JaCoCo HTML/XML report, lint output | Sprint 3 |
| NFR-A-01 | **Lighthouse CI** accessibility category + **axe-core** (`@axe-core/cli`) on the main screens | `frontend.yml` + manual contrast review | Lighthouse/axe reports | Sprint 4 |
| NFR-A-02 | Manual keyboard-only navigation checklist (`Tab`, `Shift+Tab`, `Enter`, `Space`, visible focus) across the `US-01`–`US-07` screens | Manual QA pass before each release | Completed checklist linked here | Sprint 4 |

### 3.2 Planned CI Changes for Sprint 3

The workflows below are specified so they can be added directly as GitHub Actions files in Sprint 3.
All of them run on `pull_request` targeting `develop` and `main`, and on `push` to `develop`.

1. **`validate-openapi.yml` (keep, small change)** — keep the Redocly lint; pin the CLI version
   (`@redocly/cli@<pinned>`) so lint results do not change between runs.
2. **`ci.yml` (new) — backend build and test**
   - `build-test` job: `actions/checkout@v4` → `actions/setup-java@v4` (Temurin 21, Maven cache) → `mvn -B verify`.
   - `mvn verify` runs unit tests (Surefire), integration tests with Testcontainers PostgreSQL (Failsafe), Checkstyle, SpotBugs, and the JaCoCo `check` goal.
   - Coverage threshold (validation target, from NFR-M-02): **≥ 70% line coverage** on the core backend domain and service classes. The build fails below the threshold.
   - Upload the JaCoCo and test reports with `actions/upload-artifact@v4`.
3. **`ci.yml` → `contract` job (new)** — depends on `build-test`; starts the API with the local JWT stub, then runs Schemathesis against `api/openapi.yaml` to check that responses match the documented schemas and status codes (400, 401, 403, 404, 409).
4. **`frontend.yml` (new, once the framework is chosen)** — install, ESLint, unit tests, production build, then Lighthouse CI (performance and accessibility) and axe-core against the built app.
5. **`load-test.yml` (new, Sprint 4)** — manual `workflow_dispatch` that runs the k6 scenario from 3.3 against a given base URL and uploads the summary.

After the workflows exist, the `main` and `develop` branch rulesets are updated so that `lint`, `build-test`, and `contract` are **required status checks**.

### 3.3 Demo-Day Load-Test Scenario (Scalability Verification)

The demo day is used as the scalability verification event for NFR-P-01, at class scale.

- **Load profile (validation target):** ramp to **50 concurrent virtual users** over 1 minute, hold for 5 minutes, ramp down over 1 minute. 50 VUs covers a full class session using the system at the same time.
- **User mix per virtual user:** 60% browse the public feed and search groups (read), 25% view a group detail page (read), 15% write operations with a test JWT (create profile, join or assign a role, advance a milestone).
- **Pass criteria (validation targets, from NFR-P-01):** p95 response time **< 300 ms** for public read endpoints (`GET /tags`, `GET /groups`, `GET /feed/projects`) and **< 500 ms** for authenticated write endpoints (`POST`/`PATCH`); HTTP 5xx error rate **< 1%** (expected 4xx answers from the scenario are not errors); no inconsistent state afterwards (checked with the NFR-R-01 queries).
- **Procedure:** run the scenario once against the staging deployment the day before (dry run), then during the demo with the class as real users while k6 adds background load. Both k6 summaries are linked in this section.
- **Test data:** a seeded dataset of tags, profiles, and groups; test accounts come from the local JWT stub or a test tenant of the identity provider, never real user accounts.

### 3.4 Pull Request Quality Gate (Sprint 3 onwards)

A pull request may be merged only when every item is true:

- [ ] The PR targets `develop` (or `main` only for a release/hotfix PR) and references its issue (`Refs #N` / `Closes #N`).
- [ ] Commit messages follow Conventional Commits (`docs/04-git-flow-policy.md`).
- [ ] All required checks are green: `lint` (OpenAPI), `build-test`, `contract`, and `frontend` when frontend files changed.
- [ ] Coverage does not fall below the current threshold, and new domain rules come with tests (including 401/403/409 cases where they apply).
- [ ] `api/openapi.yaml` is updated in the same PR when an endpoint, schema, or status code changes.
- [ ] At least one approval from the accountable reviewer; no unresolved review comments.
- [ ] No secrets, credentials, or real user data in the diff.

## 4. Quality Measurement Rules

1. Every NFR names a criterion and a verification method; no exceptions.
2. Unverified numbers are labeled **validation targets**, never reported as achieved.
3. A quality claim is only "met" when the verification method has actually run and its evidence is linked here.
4. Quality claims must not contradict `api/openapi.yaml` or the Sprint 1 boundary.
