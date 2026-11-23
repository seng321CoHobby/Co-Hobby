# Sprint 2 Assessment Checklist

**Course:** SENG 321 Software Engineering
**Team:** 19
**Project:** Co-Hobby
**Sprint:** 2 (due 2026-11-24 23:59)
**Status:** Ready for review — authored by @xa1res (Issue #24, PROC-01); reviewer @Bruhun; used by @yigitozkaya07 in the QA-01 sweep (Issue #35)

> The Sprint 2 assignment asks us to comply with the "official BM321 Software Engineering
> Semester Team Project Specification and Assessment Rubric". No official rubric has been
> shared with the team, so this checklist is our own version of it, built from the sources in §1,
> and it is the reference for the QA-01 sweep (#35) and the release (#37).

## 1. Sources

| ID | Source | Used for |
|---|---|---|
| SRC-1 | Sprint 2 assignment text on Microsoft Teams ("Sprint 2 – Requirements & Architecture") | §2 deliverables, §3 submission requirements, §4 process rules |
| SRC-2 | Sprint 1 assignment text on Microsoft Teams ("Sprint 1 – Project Foundation & Team Operating Model") | §4 traceability rules and §5 consistency with Sprint 1 work |
| SRC-3 | Lecturer's "Sprint 1 Examples" pack (Teams Files), as applied in [`seng_321_sprint_1_submission.md`](seng_321_sprint_1_submission.md) | §6 report structure and peer-review exercise style |
| SRC-4 | Team agreements: [`04-git-flow-policy.md`](04-git-flow-policy.md) and the Sprint 2 issues #24–#38 | §4 process rules, §7 contribution balance |

**Official rubric:** not available; only the assignment texts and the Sprint 1 examples were shared. This checklist applies instead.

## 2. Required Deliverables (SRC-1)

**How to use this table:** the Status column shows the state on 2026-11-23. In the QA-01 sweep (#35), tick the **QA** box only after checking the file on `develop`, not on a feature branch.

Legend: ✅ merged into `develop` · 🟡 open pull request · 🔴 no pull request yet

### D1 — Detailed SRS and refined Product Backlog

| ID | Check | Evidence | Issue / PR | Status | QA |
|---|---|---|---|---|---|
| D1.1 | The SRS has an introduction (purpose, scope, definitions, references), an overall description, functional requirements, use cases, data requirements and interface requirements. | [`06-srs.md`](06-srs.md) §1–§6 | #26 / PR #42 | ✅ | [ ] |
| D1.2 | Every functional requirement traces to a user story, a use case and an API operation. | `06-srs.md` §8 | #26 / PR #42 | ✅ | [ ] |
| D1.3 | The SRS links the NFR document and the UML models. | `06-srs.md` §7, §9 | #26, #33 / PR #42, PR #46 | ✅ | [ ] |
| D1.4 | The backlog has re-validated priorities and estimates, and acceptance criteria that cover the SRS error flows (400/401/403/404/409). | [`05-product-backlog.md`](05-product-backlog.md) | #27 / PR #44 | 🟡 | [ ] |
| D1.5 | The backlog has a Definition of Done and an implementation order for Sprint 3. | `05-product-backlog.md` | #27 / PR #44 | 🟡 | [ ] |
| D1.6 | The backlog still contains exactly US-01 to US-07, with no new scope. | `05-product-backlog.md` | #27 / PR #44 | 🟡 | [ ] |

### D2 — Non-functional requirements and quality-measure specifications

| ID | Check | Evidence | Issue / PR | Status | QA |
|---|---|---|---|---|---|
| D2.1 | The NFR catalogue covers performance, security, usability, reliability, maintainability and accessibility. Each NFR has an ID and a measurable target. | [`07-nfr-quality-measures.md`](07-nfr-quality-measures.md) §2 | #28 / PR #43 | 🟡 | [ ] |
| D2.2 | Quality measurement rules state how and when each target is measured. | `07-nfr-quality-measures.md` §4 | #28 / PR #43 | 🟡 | [ ] |
| D2.3 | Each NFR names its verification tool, for example the OpenAPI lint, JUnit coverage, a load-test tool or Lighthouse. | `07-nfr-quality-measures.md` §3 | #29 | 🔴 | [ ] |
| D2.4 | The planned CI changes for Sprint 3 are listed, along with the demo-day load-test scenario and a PR quality-gate checklist. | `07-nfr-quality-measures.md` §3 | #29 | 🔴 | [ ] |
| D2.5 | The NFR IDs cited by the architecture design decisions (NFR-P-01, NFR-S-01…03, NFR-R-01, NFR-M-01…02) exist in the catalogue. | `08-architecture.md` §4 vs `07-...md` §2 | #28, #32 | 🟡 | [ ] |
| D2.6 | No `<TODO>` markers are left in the file. | `07-nfr-quality-measures.md` | #28, #29 | 🔴 | [ ] |

### D3 — UI/UX prototypes in Figma, including user-flow diagrams

| ID | Check | Evidence | Issue / PR | Status | QA |
|---|---|---|---|---|---|
| D3.1 | The Figma file is public and view-only, and it opens from a logged-out browser. | [`09-ui-ux.md`](09-ui-ux.md) §1 | #30 / PR #47 | 🟡 | [ ] |
| D3.2 | There are high-fidelity screens for every first-release story (US-01 to US-07), each with a committed PNG export. | `09-ui-ux.md` §2, `docs/figma/` | #30 / PR #47 | 🟡 | [ ] |
| D3.3 | Every screen maps to a user story, a use case, an FR and an API operation. Loading, empty and error states are shown. | `09-ui-ux.md` §2, §2.1 | #30 / PR #47 | 🟡 | [ ] |
| D3.4 | No screen shows deferred scope (chat, swipe, self-join, payments, notifications). | `09-ui-ux.md` §2.2 | #30 / PR #47 | 🟡 | [ ] |
| D3.5 | There are three user-flow diagrams (find a group, create a group and fill vacancies, project milestones and sharing), drawn in Figma or FigJam, each with a committed PNG and a short narration. | `09-ui-ux.md` §3, `docs/diagrams/user-flow-*.png` | #31 | 🔴 | [ ] |
| D3.6 | No `<TODO>` markers are left in the file. | `09-ui-ux.md` | #30, #31 | 🔴 | [ ] |

### D4 — Software architecture documentation (C4 and UML)

| ID | Check | Evidence | Issue / PR | Status | QA |
|---|---|---|---|---|---|
| D4.1 | There is a C4 Level 1 (System Context) diagram, consistent with the Sprint 1 boundary. | [`08-architecture.md`](08-architecture.md) §3.1, `diagrams/c4-context.*` | #32, #38 / PR #39, PR #45 | ✅ | [ ] |
| D4.2 | There is a C4 Level 2 (Containers) diagram, with its protocols and authentication notes. | `08-architecture.md` §3.2, `diagrams/c4-containers.*` | #32 / PR #45 | ✅ | [ ] |
| D4.3 | The decision on C4 Level 3 is documented. It is currently omitted with a rationale; revisit this if the official rubric asks for Level 3. | `08-architecture.md` §3.3 | #32 / PR #45 | ✅ | [ ] |
| D4.4 | Each design decision has its context, decision, rationale, consequences and the NFRs that drove it. | `08-architecture.md` §4 (DD-01…DD-04) | #32 / PR #45 | ✅ | [ ] |
| D4.5 | There is a UML class diagram of the domain. | `diagrams/uml-class.*` | #34 / PR #40 | ✅ | [ ] |
| D4.6 | There are UML sequence diagrams for `addGroupMember` and `updateProjectProgress`, and their notes match the current contract. | `diagrams/uml-seq-*.*` | #34 / PR #40, PR #41, PR #48 | 🟡 | [ ] |
| D4.7 | There is a UML use-case diagram covering US-01 to US-07. | `diagrams/uml-use-case.*` | #33 / PR #46 | ✅ | [ ] |
| D4.8 | There is a UML state diagram for the milestone lifecycle (PLANNING → WEEK_1 → WEEK_2 → COMPLETED). | `diagrams/uml-state.*` | #33 / PR #46 | ✅ | [ ] |
| D4.9 | Every diagram is committed as a source file and a PNG export, and is linked from `08-architecture.md` §5. The old #33 placeholder line in §5, which now repeats §5.1, should be removed (noted in the PR #46 review). | `docs/diagrams/`, `08-architecture.md` §5 | #32–#34 | 🟡 | [ ] |

## 3. Submission Requirements (SRC-1)

| ID | Check | Evidence | Issue | Status | QA |
|---|---|---|---|---|---|
| S1 | Team information is given: team number, project name, and members with student numbers and GitHub accounts. | `seng_321_sprint_2_submission.md` | #36 | 🔴 | [ ] |
| S2 | The report links the GitHub repository: <https://github.com/seng321CoHobby/Co-Hobby> | `seng_321_sprint_2_submission.md` | #36 | 🔴 | [ ] |
| S3 | The report gives the release and tag information: the `sprint-2` tag on `main` and its GitHub Release. | `seng_321_sprint_2_submission.md`, Releases page | #37 | 🔴 | [ ] |
| S4 | The report gives each member's name and Sprint 2 responsibilities. | `seng_321_sprint_2_submission.md`, `CONTRIBUTIONS.md` | #36 | 🔴 | [ ] |
| S5 | The report links the relevant issues, pull requests, technical documents, diagrams and the Figma file. | Traceability table in the report | #36 | 🔴 | [ ] |
| S6 | Every link in the report resolves from a logged-out browser. | QA-01 sweep | #35 | 🔴 | [ ] |
| S7 | The report is uploaded to the Teams assignment before 2026-11-24 23:59. | Teams submission | #37 | 🔴 | [ ] |

## 4. Process and GitHub Evidence (SRC-1, SRC-2, SRC-4)

| ID | Check | How to verify | Status | QA |
|---|---|---|---|---|
| P1 | Repository history stays intact: no force-push, history rewrite or squash on `main` or `develop`. | Inspect the commit graph; compare `sprint-1` with `main` | ✅ so far | [ ] |
| P2 | Every Sprint 2 pull request targets `develop`, references its issue (`Refs #N`) and has at least one approval before merge. | Closed PR list | ✅ for merged PRs | [ ] |
| P3 | Commits follow Conventional Commits (`docs:`, `feat:`, `fix:`, …) and reference the issue where applicable. | `git log origin/main..origin/develop` | ✅ so far | [ ] |
| P4 | The OpenAPI lint workflow passes on every pull request that changes `api/openapi.yaml`. | Actions tab | ✅ | [ ] |
| P5 | Every Sprint 2 issue (#24–#38) has the `sprint-2` label, an area label and the Sprint 2 milestone. | Issue list filtered by milestone | ✅ | [ ] |
| P6 | Every commit author email is linked to the member's GitHub account, so contributions show up under their username. | Commit list on GitHub (author avatar or login present) | ✅ for `develop` | [ ] |
| P7 | Demo and template files are removed (`index.html` and `package.json` are still in the root). | Repository root | 🔴 #25 | [ ] |
| P8 | The release follows this order: all Sprint 2 PRs merged into `develop`, then a reviewed release PR from `develop` to `main`, then the `sprint-2` tag and GitHub Release, then the final links in the report. | #37 | 🔴 | [ ] |
| P9 | Issues are closed by the release PR only after their evidence is merged. | Issue list after the release | 🔴 #37 | [ ] |

## 5. Consistency with Sprint 1 (SRC-2)

The Sprint 1 assignment requires documentation and GitHub evidence to stay consistent. Check each Sprint 2 document against the Sprint 1 baseline:

| ID | Check | Baseline | QA |
|---|---|---|---|
| C1 | No new actors, external systems or responsibilities have been added. | [`02-vision-and-boundary.md`](02-vision-and-boundary.md) | [ ] |
| C2 | No deferred feature has been re-introduced: chat, swipe matching, calls, payments, notifications, GPS, admin panels, raw media hosting or an identity-provider implementation. | [`01-project-proposal.md`](01-project-proposal.md) "Deferred" | [ ] |
| C3 | Requirements, screens and diagrams use only operations and status codes that exist in the contract. If a change was needed, the contract was updated in the same PR. | [`api/openapi.yaml`](../api/openapi.yaml) | [ ] |
| C4 | User story IDs, priorities and owners match across the backlog, the SRS, the Figma mapping and the use-case diagram. | [`05-product-backlog.md`](05-product-backlog.md) | [ ] |
| C5 | Member roles in the Sprint 2 documents match the role table. | [`03-roles-and-raci.md`](03-roles-and-raci.md) | [ ] |
| C6 | Milestone stage names are identical everywhere: `PLANNING`, `WEEK_1`, `WEEK_2`, `COMPLETED`. | `api/openapi.yaml` | [ ] |

## 6. Report Structure Expectations (SRC-3)

The Sprint 1 report followed the lecturer's examples pack. The Sprint 2 report (`docs/seng_321_sprint_2_submission.md`, #36) keeps the same structure:

- [ ] A **Project Information** block: project name, team number, repository URL, release tag URL, and links to the main files.
- [ ] A **Team Members** table: name, student number, GitHub account, role, and primary Sprint 2 ownership.
- [ ] One numbered section per deliverable group (D1–D4), each summarising the content and linking the full document and diagram PNGs.
- [ ] A **Sprint 2 peer-review exercise**: questions another team should be able to answer without oral explanation, plus an "internal review revision" note listing what changed after review. The proposed questions for QA-01 are below.
- [ ] A **Submission Traceability and GitHub Evidence** table: evidence, issue ID, responsible member(s) and link.
- [ ] A **References** section.
- [ ] Every Sprint 2 document keeps the Course / Team / Project / Sprint / Status header block, and the Status line names the author(s) and issue.

**Proposed Sprint 2 peer-review questions (for #35):**

1. Which functional requirements does each user story produce, and where is each one traced? (SRS §8)
2. How is each NFR measured, and which tool or test verifies it? (NFR §2–§4)
3. Can a reviewer follow a user journey from a Figma screen to the API operation it calls? (UI/UX §2–§3)
4. Which containers make up the system, and which external systems does the API depend on? (C4 L1–L2)
5. What happens when an owner fills a full vacancy or skips a milestone stage? (sequence and state diagrams, 409 paths)
6. Which story does Sprint 3 start with, and when is a story "done"? (backlog DoD and implementation order)

## 7. Contribution Balance (SRC-1, SRC-4)

**Target:** every member authors at least two Sprint 2 artifacts. Reviews count as evidence but not as authored artifacts.

Snapshot on 2026-11-23:

| Member | Authored Sprint 2 artifacts | Reviews | Meets target? |
|---|---|---|---|
| @Bruhun (Enes Alp Erkmen) | Sprint 2 skeletons and C4 L1 (PR #39 ✅), API 403 clarification (PR #41 ✅), C4 L2 and design decisions (PR #45 ✅), UML use-case and state (PR #46 ✅) | #40, #44 | ✅ |
| @bakicanerdogan (Baki Can Erdoğan) | UML class and sequence (PR #40 ✅), Figma prototypes (PR #47 🟡), sequence-note fix (PR #48 🟡); user flows (#31) pending | #39, #41, #45, #46 | 🟡 met once PR #47 is merged |
| @beyazitKRGL (Yıldırım Beyazıt Köroğlu) | SRS (PR #42 ✅) | #44 | 🔴 one authored artifact. Proposed fix: co-author #27 by adding the FR-ID column to the backlog suggested in the PR #44 review, or author part of #31 |
| @yigitozkaya07 (Hüseyin Yiğit Özkaya) | NFR catalogue (PR #43 🟡), refined backlog (PR #44 🟡); user flows (#31) and QA sweep (#35) pending | #42 | 🟡 met once PRs #43 and #44 are merged |
| @sengProje64 (Abdullah Şar) | None yet; NFR verification tooling (#29), repository cleanup (#25) and release (#37) pending | — | 🔴 no authored artifact. #29 and #25 must be opened today |
| @xa1res (Mete Dugan) | This checklist (#24); submission report and contributions (#36) pending | — | 🟡 met once #36 is merged |

Re-run this check before the release PR (#37) and copy the final state into `CONTRIBUTIONS.md` (#36).

## 8. Open Items Before the Deadline

| Order | Item | Owner | Blocks |
|---|---|---|---|
| 1 | Review and merge PR #43 (NFR catalogue) | @Bruhun (requested reviewer) | PR #44, D2, #35 |
| 2 | Open and merge the #29 PR (NFR §3 verification tooling) | @sengProje64, reviewer @yigitozkaya07 | D2.3, D2.4, D2.6 |
| 3 | Merge PR #44 after PR #43 (refined backlog and DoD) | @yigitozkaya07; label and body fixes requested by @Bruhun | D1.4–D1.6 |
| 4 | Review and merge PR #47 (Figma prototypes) | @beyazitKRGL (requested reviewer) | D3.1–D3.4 |
| 5 | Open and merge the #31 PR (user-flow diagrams) | @yigitozkaya07, @bakicanerdogan | D3.5, D3.6 |
| 6 | Review and merge PR #48 (sequence-note fix) | @Bruhun (requested reviewer) | D4.6 |
| 7 | Open and merge the #25 PR (remove `index.html`, `package.json`; fix metadata) | @Bruhun, @sengProje64 | P7 |
| 8 | QA-01 sweep against this checklist | @yigitozkaya07, reviewer @xa1res | #36 peer-review section, #37 |
| 9 | Submission report and `CONTRIBUTIONS.md` | @xa1res, @yigitozkaya07 | S1, S2, S4, S5, #37 |
| 10 | Release PR, `sprint-2` tag, GitHub Release, final links, Teams upload | @sengProje64, reviewer @xa1res | S3, S6, S7 |
