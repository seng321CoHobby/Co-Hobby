# Non-Functional Requirements and Quality-Measure Specifications

**Course:** SENG 321 Software Engineering
**Team:** 19
**Project:** Co-Hobby
**Sprint:** 2
**Status:** Draft — skeleton prepared by @Bruhun, authored by @yigitozkaya07 (Issue #28) with a verification-tooling section by @sengProje64 (Issue #29)

> Define quality in terms of *measurable criteria and verification methods*, not claims.
> The system is not yet implemented: numeric values are **validation targets** for later
> sprints (Sprint 3–4), never assertions the current team must prove now. Avoid bare SLAs
> with no measurement plan.
> This document must exist **before** `docs/08-architecture.md` is finalized (NFRs drive the
> C4 design decisions).

## 1. Purpose

<TODO: why quality measures matter for the first release and how they will be verified.>

## 2. NFR Catalogue

> Fill one row per NFR. Every row needs a measurable criterion **and** a verification method.

### 2.1 Performance

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-P-01 | API endpoints respond within a bounded latency under expected load. | <TODO: p95 latency target under a defined load> | JMeter (or k6) load test against the deployed API | Sprint 4 |
| NFR-P-02 | Public feed loads without blocking the UI. | <TODO> | <TODO: browser timing / Lighthouse> | Sprint 4 |

### 2.2 Security

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-S-01 | All write operations require a valid JWT. | 100% of write endpoints reject requests without a valid token. | API integration tests (401 cases), matching `api/openapi.yaml` | Sprint 3 |
| NFR-S-02 | OWNER-restricted mutations reject non-owners. | All restricted operations return 403 for non-owners. | API integration tests (403 cases) | Sprint 3 |
| NFR-S-03 | External media references are bounded and validated. | Only well-formed URIs are accepted; invalid URLs return 400. | Contract tests on mediaUrls schema | Sprint 3 |

### 2.3 Usability

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-U-01 | A new hobbyist can find a compatible group quickly. | Group discovery completes in **under three minutes** in a moderated usability test (from the Sprint 1 proposal). | Moderated usability test with the Figma prototype and later the web app; record task time and success rate | Sprint 3 / Sprint 4 |
| NFR-U-02 | Users understand group vacancies without asking the owner. | <TODO: vacancy/role visibility measure> | Usability test scenario, success rate metric | Sprint 4 |

### 2.4 Reliability

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-R-01 | Domain rules never allow invalid state (duplicate members, filled vacancies, skipped stages). | All 409-path cases return errors; no inconsistent state persists. | API integration tests (409 cases) | Sprint 3 |
| NFR-R-02 | <TODO: data integrity / error handling measure> | <TODO> | <TODO> | <TODO> |

### 2.5 Maintainability

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-M-01 | API contract remains valid and consistent. | OpenAPI lint passes on every PR (no errors). | Existing Redocly workflow `.github/workflows/validate-openapi.yml` | Sprint 2 → 4 |
| NFR-M-02 | Codebase stays testable and reviewable. | <TODO: unit-test coverage target and lint rules> | CI coverage report, lint workflow | Sprint 3 |

### 2.6 Accessibility

| ID | Requirement | Measurable Criterion | Verification Method (Tool / Technique) | Target Sprint |
|---|---|---|---|---|
| NFR-A-01 | UI is accessible to common assistive technologies. | <TODO: WCAG 2.1 AA checklist + measured score target> | Lighthouse accessibility audit, keyboard-navigation test on the prototype and web app | Sprint 4 |

## 3. Quality Verification Tooling and Test Plans (Issue #29 — DevOps)

This section turns the NFR catalogue into concrete tools, CI steps, and test events. Everything
here is a **plan for Sprint 3–4**: only the OpenAPI lint workflow exists today. A measure counts
as "met" only after the listed tool has run and its evidence (CI run link, report artifact) is
linked here (rule 3 in Section 4).

### 3.1 Verification Tool per NFR

| NFR | Verification tool | Where it runs | Evidence produced | Becomes active |
|---|---|---|---|---|
| NFR-P-01 | **k6** load script (`perf/api-load.js`) against the deployed API; JMeter accepted as an alternative | Manual workflow (`workflow_dispatch`) + demo-day load test (3.3) | k6 summary (p95 latency, error rate) uploaded as a workflow artifact | Sprint 4 |
| NFR-P-02 | **Lighthouse CI** (`@lhci/cli`) performance category on the feed page | `frontend.yml` on PRs touching the frontend | Lighthouse report (performance score, LCP, TBT) as artifact | Sprint 4 |
| NFR-S-01 | **JUnit 5 + Spring Boot Test (MockMvc)** integration tests: every write endpoint called without/with an invalid JWT must return 401 | `ci.yml` → `mvn verify` | Surefire/Failsafe test report | Sprint 3 |
| NFR-S-02 | JUnit 5 + MockMvc: every OWNER-only operation called by a non-owner must return 403 | `ci.yml` → `mvn verify` | Test report | Sprint 3 |
| NFR-S-03 | Contract tests on the `mediaUrls` schema (invalid URI → 400) plus **Schemathesis** run against the running API | `ci.yml` → `contract` job | Schemathesis report, test report | Sprint 3 |
| NFR-U-01 | Moderated usability test (prototype in Sprint 3, web app in Sprint 4) with a recorded task-time sheet | Manual, organized by QA | Task time and success-rate table linked from this document | Sprint 3 / 4 |
| NFR-U-02 | Usability test scenario "find a group that needs my role" | Manual, organized by QA | Success-rate table | Sprint 4 |
| NFR-R-01 | JUnit 5 + **Testcontainers (PostgreSQL)** integration tests for every 409 path (duplicate member, filled vacancy, skipped stage, share before `COMPLETED`), including a concurrent-request test for the same vacancy | `ci.yml` → `mvn verify` | Test report | Sprint 3 |
| NFR-M-01 | **Redocly CLI** lint of `api/openapi.yaml` (existing `validate-openapi.yml`) | Every PR touching `api/openapi.yaml` | Workflow check status | Active now |
| NFR-M-02 | **JaCoCo** coverage report with a minimum-coverage rule; **Checkstyle** (Google style) for the backend; ESLint for the frontend | `ci.yml` / `frontend.yml` | JaCoCo HTML/XML report, lint output | Sprint 3 |
| NFR-A-01 | **Lighthouse CI** accessibility category + **axe-core** (`@axe-core/cli`) on the main screens, plus a manual keyboard-navigation checklist | `frontend.yml` + manual QA pass | Lighthouse/axe reports, completed checklist | Sprint 4 |

### 3.2 Planned CI Changes for Sprint 3

The workflows below are specified so they can be added directly as GitHub Actions files in Sprint 3.
All of them run on `pull_request` targeting `develop` and `main`, and on `push` to `develop`.

1. **`validate-openapi.yml` (keep, small change)** — keep the Redocly lint; pin the CLI version
   (`@redocly/cli@<pinned>`) so lint results do not change between runs.
2. **`ci.yml` (new) — backend build and test**
   - `build-test` job: `actions/checkout@v4` → `actions/setup-java@v4` (Temurin 21, Maven cache) → `mvn -B verify`.
   - `mvn verify` runs unit tests (Surefire), integration tests with Testcontainers PostgreSQL (Failsafe), Checkstyle, and the JaCoCo `check` goal.
   - Coverage threshold (validation target): **≥ 70% line coverage** on the service layer in Sprint 3, raised to **≥ 80%** in Sprint 4. The build fails below the threshold.
   - Upload the JaCoCo and test reports with `actions/upload-artifact@v4`.
3. **`ci.yml` → `contract` job (new)** — depends on `build-test`; starts the API with the local JWT stub, then runs Schemathesis against `api/openapi.yaml` to check that responses match the documented schemas and status codes (400, 401, 403, 404, 409).
4. **`frontend.yml` (new, once the framework is chosen)** — install, ESLint, unit tests, production build, then Lighthouse CI (performance and accessibility) and axe-core against the built app.
5. **`load-test.yml` (new, Sprint 4)** — manual `workflow_dispatch` that runs the k6 scenario from 3.3 against a given base URL and uploads the summary.

After the workflows exist, the `main` and `develop` branch rulesets are updated so that `lint`, `build-test`, and `contract` are **required status checks**.

### 3.3 Demo-Day Load-Test Scenario (Scalability Verification)

The demo day is used as the scalability verification event for NFR-P-01, at class scale.

- **Load profile (validation target):** ramp to **50 concurrent virtual users** over 1 minute, hold for 5 minutes, ramp down over 1 minute. 50 VUs covers a full class session using the system at the same time.
- **User mix per virtual user:** 60% browse the public feed and search groups (read), 25% view a group detail page (read), 15% write operations with a test JWT (create profile, join or assign a role, advance a milestone).
- **Pass criteria (validation targets):** p95 latency **< 500 ms** for read endpoints and **< 1 s** for write endpoints; error rate **< 1%** (expected 4xx answers from the scenario are not counted as errors); no inconsistent state afterwards (checked with the NFR-R-01 queries).
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
