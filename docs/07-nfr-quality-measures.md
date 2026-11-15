# Non-Functional Requirements and Quality-Measure Specifications

**Course:** BM321 Software Engineering
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
