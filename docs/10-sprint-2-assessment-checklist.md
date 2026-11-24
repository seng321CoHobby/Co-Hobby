# Sprint 2 Assessment Checklist

**Course:** SENG 321 Software Engineering
**Team:** 19
**Project:** Co-Hobby
**Sprint:** 2 (due 2026-11-24 23:59)
**Status:** QA-01 sweep completed on 2026-11-23 — authored by @xa1res (Issue #24, PROC-01); reviewer @Bruhun; verified by @yigitozkaya07 in the QA-01 sweep (Issue #35)

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

**How to use this table:** Status and QA columns reflect the QA-01 sweep on `develop` (2026-11-23). Release items (`#37`) were updated after OPS-04 published the `sprint-2` tag on 2026-11-23; only the Teams upload (S7) is still open.

Legend: ✅ merged into `develop` · 🟡 open pull request · 🔴 no pull request yet

### D1 — Detailed SRS and refined Product Backlog

| ID | Check | Evidence | Issue / PR | Status | QA |
|---|---|---|---|---|---|
| D1.1 | The SRS has an introduction (purpose, scope, definitions, references), an overall description, functional requirements, use cases, data requirements and interface requirements. | [`06-srs.md`](06-srs.md) §1–§6 | #26 / PR #42 | ✅ | [x] |
| D1.2 | Every functional requirement traces to a user story, a use case and an API operation. | `06-srs.md` §8 | #26 / PR #42 | ✅ | [x] |
| D1.3 | The SRS links the NFR document and the UML models. | `06-srs.md` §7, §9 | #26, #33 / PR #42, PR #46 | ✅ | [x] |
| D1.4 | The backlog has re-validated priorities and estimates, and acceptance criteria that cover the SRS error flows (400/401/403/404/409). | [`05-product-backlog.md`](05-product-backlog.md) | #27 / PR #44 | ✅ | [x] |
| D1.5 | The backlog has a Definition of Done and an implementation order for Sprint 3. | `05-product-backlog.md` | #27 / PR #44 | ✅ | [x] |
| D1.6 | The backlog still contains exactly US-01 to US-07, with no new scope. | `05-product-backlog.md` | #27 / PR #44 | ✅ | [x] |

### D2 — Non-functional requirements and quality-measure specifications

| ID | Check | Evidence | Issue / PR | Status | QA |
|---|---|---|---|---|---|
| D2.1 | The NFR catalogue covers performance, security, usability, reliability, maintainability and accessibility. Each NFR has an ID and a measurable target. | [`07-nfr-quality-measures.md`](07-nfr-quality-measures.md) §2 | #28 / PR #43 | ✅ | [x] |
| D2.2 | Quality measurement rules state how and when each target is measured. | `07-nfr-quality-measures.md` §4 | #28 / PR #43 | ✅ | [x] |
| D2.3 | Each NFR names its verification tool, for example the OpenAPI lint, JUnit coverage, a load-test tool or Lighthouse. | `07-nfr-quality-measures.md` §3 | #29 / PR #51 | ✅ | [x] |
| D2.4 | The planned CI changes for Sprint 3 are listed, along with the demo-day load-test scenario and a PR quality-gate checklist. | `07-nfr-quality-measures.md` §3 | #29 / PR #51 | ✅ | [x] |
| D2.5 | The NFR IDs cited by the architecture design decisions (NFR-P-01, NFR-S-01…03, NFR-R-01, NFR-M-01…02) exist in the catalogue. | `08-architecture.md` §4 vs `07-...md` §2 | #28, #32 / PR #43, PR #45 | ✅ | [x] |
| D2.6 | No `<TODO>` markers are left in the file. | `07-nfr-quality-measures.md` | #28, #29 / PR #43, PR #51 | ✅ | [x] |

### D3 — UI/UX prototypes in Figma, including user-flow diagrams

| ID | Check | Evidence | Issue / PR | Status | QA |
|---|---|---|---|---|---|
| D3.1 | The Figma file is public and view-only, and it opens from a logged-out browser. | [`09-ui-ux.md`](09-ui-ux.md) §1 (verified in incognito mode) | #30 / PR #47 | ✅ | [x] |
| D3.2 | There are high-fidelity screens for every first-release story (US-01 to US-07), each with a committed PNG export. | `09-ui-ux.md` §2, `docs/figma/` | #30 / PR #47 | ✅ | [x] |
| D3.3 | Every screen maps to a user story, a use case, an FR and an API operation. Loading, empty and error states are shown. | `09-ui-ux.md` §2, §2.1 | #30 / PR #47 | ✅ | [x] |
| D3.4 | No screen shows deferred scope (chat, swipe, self-join, payments, notifications). | `09-ui-ux.md` §2.2 | #30 / PR #47 | ✅ | [x] |
| D3.5 | There are three user-flow diagrams (find a group, create a group and fill vacancies, project milestones and sharing), drawn in Figma or FigJam, each with a committed PNG and a short narration. | `09-ui-ux.md` §3, `docs/diagrams/user-flow-*.png` | #31 / PR #50 | ✅ | [x] |
| D3.6 | No `<TODO>` markers are left in the file. | `09-ui-ux.md` | #30, #31 / PR #47, PR #50 | ✅ | [x] |

### D4 — Software architecture documentation (C4 and UML)

| ID | Check | Evidence | Issue / PR | Status | QA |
|---|---|---|---|---|---|
| D4.1 | There is a C4 Level 1 (System Context) diagram, consistent with the Sprint 1 boundary. | [`08-architecture.md`](08-architecture.md) §3.1, `diagrams/c4-context.*` | #32, #38 / PR #39, PR #45 | ✅ | [x] |
| D4.2 | There is a C4 Level 2 (Containers) diagram, with its protocols and authentication notes. | `08-architecture.md` §3.2, `diagrams/c4-containers.*` | #32 / PR #45 | ✅ | [x] |
| D4.3 | The decision on C4 Level 3 is documented. It is currently omitted with a rationale; revisit this if the official rubric asks for Level 3. | `08-architecture.md` §3.3 | #32 / PR #45 | ✅ | [x] |
| D4.4 | Each design decision has its context, decision, rationale, consequences and the NFRs that drove it. | `08-architecture.md` §4 (DD-01…DD-04) | #32 / PR #45 | ✅ | [x] |
| D4.5 | There is a UML class diagram of the domain. | `diagrams/uml-class.*` | #34 / PR #40 | ✅ | [x] |
| D4.6 | There are UML sequence diagrams for `addGroupMember` and `updateProjectProgress`, and their notes match the current contract. | `diagrams/uml-seq-*.*` | #34 / PR #40, PR #41, PR #48 | ✅ | [x] |
| D4.7 | There is a UML use-case diagram covering US-01 to US-07. | `diagrams/uml-use-case.*` | #33 / PR #46 | ✅ | [x] |
| D4.8 | There is a UML state diagram for the milestone lifecycle (PLANNING → WEEK_1 → WEEK_2 → COMPLETED). | `diagrams/uml-state.*` | #33 / PR #46 | ✅ | [x] |
| D4.9 | Every diagram is committed as a source file and a PNG export, and is linked from `08-architecture.md` §5. | `docs/diagrams/`, `08-architecture.md` §5 | #32–#34 / PR #39, #40, #45, #46, #48 | ✅ | [x] |

## 3. Submission Requirements (SRC-1)

| ID | Check | Evidence | Issue / PR | Status | QA |
|---|---|---|---|---|---|
| S1 | Team information is given: team number, project name, and members with student numbers and GitHub accounts. | `seng_321_sprint_2_submission.md` | #36 / PR #53 | ✅ | [x] |
| S2 | The report links the GitHub repository: <https://github.com/seng321CoHobby/Co-Hobby> | `seng_321_sprint_2_submission.md` | #36 / PR #53 | ✅ | [x] |
| S3 | The report gives the release and tag information: the `sprint-2` tag on `main` and its GitHub Release. | `seng_321_sprint_2_submission.md`, Releases page | #37 / PR #54, PR #55 | ✅ | [x] |
| S4 | The report gives each member's name and Sprint 2 responsibilities. | `seng_321_sprint_2_submission.md`, `CONTRIBUTIONS.md` | #36 / PR #53 | ✅ | [x] |
| S5 | The report links the relevant issues, pull requests, technical documents, diagrams and the Figma file. | Traceability table in the report | #36 / PR #53 | ✅ | [x] |
| S6 | Every link in the report resolves from a logged-out browser. | QA-01 sweep (public repo and Figma view-only link verified in incognito mode; `sprint-2` tag URL resolves once #37 publishes) | #35 | ✅ | [x] |
| S7 | The report is uploaded to the Teams assignment before 2026-11-24 23:59. | Teams submission | #37 | 🟡 | [ ] |

## 4. Process and GitHub Evidence (SRC-1, SRC-2, SRC-4)

| ID | Check | How to verify | Status | QA |
|---|---|---|---|---|
| P1 | Repository history stays intact: no force-push, history rewrite or squash on `main` or `develop`. | Inspect the commit graph; compare `sprint-1` with `main` | ✅ | [x] |
| P2 | Every Sprint 2 pull request targets `develop`, references its issue (`Refs #N`) and has at least one approval before merge. | Closed PR list (#39–#53) | ✅ | [x] |
| P3 | Commits follow Conventional Commits (`docs:`, `feat:`, `fix:`, …) and reference the issue where applicable. | `git log origin/main..origin/develop` | ✅ | [x] |
| P4 | The OpenAPI lint workflow passes on every pull request that changes `api/openapi.yaml`. | Actions tab (PR #41 green) | ✅ | [x] |
| P5 | Every Sprint 2 issue (#24–#38) has the `sprint-2` label, an area label and the Sprint 2 milestone. | Issue list filtered by milestone | ✅ | [x] |
| P6 | Every commit author email is linked to the member's GitHub account, so contributions show up under their username. | Commit list on GitHub (`@xekone1` historical note documented in `CONTRIBUTIONS.md`) | ✅ | [x] |
| P7 | Demo and template files are removed (`index.html` and `package.json` removed from root). | Repository root (#25 / PR #52) | ✅ | [x] |
| P8 | The release follows this order: all Sprint 2 PRs merged into `develop`, then a reviewed release PR from `develop` to `main`, then the `sprint-2` tag and GitHub Release, then the final links in the report. | #37 / PR #54, PR #55 | ✅ | [x] |
| P9 | Issues are closed by the release PR only after their evidence is merged. | Issue list after the release (#37) | ✅ | [x] |

## 5. Consistency with Sprint 1 (SRC-2)

The Sprint 1 assignment requires documentation and GitHub evidence to stay consistent. Check each Sprint 2 document against the Sprint 1 baseline:

| ID | Check | Baseline | QA |
|---|---|---|---|
| C1 | No new actors, external systems or responsibilities have been added. | [`02-vision-and-boundary.md`](02-vision-and-boundary.md) | [x] |
| C2 | No deferred feature has been re-introduced: chat, swipe matching, calls, payments, notifications, GPS, admin panels, raw media hosting or an identity-provider implementation. | [`01-project-proposal.md`](01-project-proposal.md) "Deferred" | [x] |
| C3 | Requirements, screens and diagrams use only operations and status codes that exist in the contract. If a change was needed, the contract was updated in the same PR. | [`api/openapi.yaml`](../api/openapi.yaml) | [x] |
| C4 | User story IDs, priorities and owners match across the backlog, the SRS, the Figma mapping and the use-case diagram. | [`05-product-backlog.md`](05-product-backlog.md) | [x] |
| C5 | Member roles in the Sprint 2 documents match the role table. | [`03-roles-and-raci.md`](03-roles-and-raci.md) | [x] |
| C6 | Milestone stage names are identical everywhere: `PLANNING`, `WEEK_1`, `WEEK_2`, `COMPLETED`. | `api/openapi.yaml` | [x] |

## 6. Report Structure Expectations (SRC-3)

The Sprint 1 report followed the lecturer's examples pack. The Sprint 2 report (`docs/seng_321_sprint_2_submission.md`, #36) keeps the same structure:

- [x] A **Project Information** block: project name, team number, repository URL, release tag URL, and links to the main files.
- [x] A **Team Members** table: name, student number, GitHub account, role, and primary Sprint 2 ownership.
- [x] One numbered section per deliverable group (D1–D4), each summarising the content and linking the full document and diagram PNGs.
- [x] A **Sprint 2 peer-review exercise**: questions another team should be able to answer without oral explanation, plus an "internal review revision" note listing what changed after review (completed in §8 via #35).
- [x] A **Submission Traceability and GitHub Evidence** table: evidence, issue ID, responsible member(s) and link.
- [x] A **References** section.
- [x] Every Sprint 2 document keeps the Course / Team / Project / Sprint / Status header block, and the Status line names the author(s) and issue.

**Proposed Sprint 2 peer-review questions (answered in `docs/seng_321_sprint_2_submission.md` §8):**

1. Which functional requirements does each user story produce, and where is each one traced? (SRS §8)
2. How is each NFR measured, and which tool or test verifies it? (NFR §2–§4)
3. Can a reviewer follow a user journey from a Figma screen to the API operation it calls? (UI/UX §2–§3)
4. Which containers make up the system, and which external systems does the API depend on? (C4 L1–L2)
5. What happens when an owner fills a full vacancy or skips a milestone stage? (sequence and state diagrams, 409 paths)
6. Which story does Sprint 3 start with, and when is a story "done"? (backlog DoD and implementation order)

## 7. Contribution Balance (SRC-1, SRC-4)

**Target:** every member authors at least two Sprint 2 artifacts. Reviews count as evidence but not as authored artifacts.

Updated QA-01 snapshot on 2026-11-23:

| Member | Authored Sprint 2 artifacts | Reviews | Meets target? |
|---|---|---|---|
| @Bruhun (Enes Alp Erkmen) | Sprint 2 skeletons and C4 L1 (PR #39 ✅), API 403 clarification (PR #41 ✅), C4 L2 and design decisions (PR #45 ✅), UML use-case and state (PR #46 ✅) | #40, #43, #44, #48, #49, #52 | ✅ |
| @bakicanerdogan (Baki Can Erdoğan) | UML class and sequence (PR #40 ✅), Figma prototypes (PR #47 ✅), sequence-note fix (PR #48 ✅), user-flow diagrams (PR #50 ✅) | #39, #41, #45, #46 | ✅ |
| @beyazitKRGL (Yıldırım Beyazıt Köroğlu) | SRS (PR #42 ✅); product input to Figma prototypes (#30) | #44, #47 | 🟡 one authored PR + product input on #30 and two PR reviews |
| @yigitozkaya07 (Hüseyin Yiğit Özkaya) | NFR catalogue (PR #43 ✅), refined backlog (PR #44 ✅), QA-01 sweep & peer-review exercise (PR #57 ✅) | #42, #50, #51, #53 | ✅ |
| @sengProje64 (Abdullah Şar) | NFR verification tooling (PR #51 ✅), repository cleanup (PR #52 ✅), Sprint 2 release (#37 / PR #54 ✅, PR #55 ✅) | — | ✅ |
| @xa1res (Mete Dugan) | Assessment checklist (PR #49 ✅), submission report and contributions (PR #53 ✅) | #54, #55, #57 | ✅ |

Final state is mirrored in `CONTRIBUTIONS.md` (#36 / #35).

## 8. Open Items Before the Deadline

| Order | Item | Owner | Status |
|---|---|---|---|
| 1 | Review and merge PR #43 (NFR catalogue) | @Bruhun / @yigitozkaya07 | ✅ Merged |
| 2 | Open and merge PR #51 (NFR §3 verification tooling) | @sengProje64 / @yigitozkaya07 | ✅ Merged |
| 3 | Merge PR #44 (refined backlog and DoD) | @yigitozkaya07 / @beyazitKRGL | ✅ Merged |
| 4 | Review and merge PR #47 (Figma prototypes) | @bakicanerdogan / @beyazitKRGL | ✅ Merged |
| 5 | Open and merge PR #50 (user-flow diagrams) | @bakicanerdogan / @yigitozkaya07 | ✅ Merged |
| 6 | Review and merge PR #48 (sequence-note fix) | @bakicanerdogan / @Bruhun | ✅ Merged |
| 7 | Open and merge PR #52 (remove `index.html`, `package.json`; metadata) | @sengProje64 / @Bruhun | ✅ Merged |
| 8 | QA-01 sweep against this checklist and peer-review exercise (#35) | @yigitozkaya07, reviewer @xa1res | ✅ Merged (PR #57) |
| 9 | Submission report and `CONTRIBUTIONS.md` (PR #53) | @xa1res / @yigitozkaya07 | ✅ Merged |
| 10 | Release PR (#54), `sprint-2` tag, GitHub Release, final links (#55), Teams upload | @sengProje64, reviewer @xa1res | ✅ Released (PR #54, PR #55, `sprint-2` tag); 🟡 Teams upload pending |
