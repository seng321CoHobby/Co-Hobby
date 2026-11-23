# SENG 321 – Individual Contributions (CONTRIBUTIONS.md)

- **Project Name:** Co-Hobby
- **Team Number:** 19
- **GitHub Repository:** https://github.com/seng321CoHobby/Co-Hobby
- **Sprint 1 Release Tag:** [`sprint-1`](https://github.com/seng321CoHobby/Co-Hobby/releases/tag/sprint-1)
- **Sprint 2 Release Tag:** `sprint-2` (placeholder until #37)

Sprint 1 contributions are listed first. Sprint 2 contributions are in [Sprint 2 – Individual Contributions](#sprint-2--individual-contributions).


---

## Summary Table of Team Members


| Name & Surname | Student Number | GitHub Username | Project Role | Assigned Issue |
|---|---|---|---|---|
| Yıldırım Beyazıt Köroğlu | 230201076 | [@beyazitKRGL](https://github.com/beyazitKRGL) | Product Owner | [Issue #1 (`DOC-01`)](https://github.com/seng321CoHobby/Co-Hobby/issues/1) |
| Mete Dugan | 240204029 | [@xa1res](https://github.com/xa1res) | Scrum Master | [Issue #4 (`DOC-03`)](https://github.com/seng321CoHobby/Co-Hobby/issues/4) |
| Enes Alp Erkmen | 240201009 | [@Bruhun](https://github.com/Bruhun) | Architect | [Issue #3 (`API-01`)](https://github.com/seng321CoHobby/Co-Hobby/issues/3) |
| Hüseyin Yiğit Özkaya | 240201052 | [@yigitozkaya07](https://github.com/yigitozkaya07) | QA Engineer | [Issue #6 (`DOC-04`)](https://github.com/seng321CoHobby/Co-Hobby/issues/6) |
| Abdullah Şar | 240201019 | [@sengProje64](https://github.com/sengProje64) | DevOps Engineer | [Issue #5 (`OPS-01`)](https://github.com/seng321CoHobby/Co-Hobby/issues/5) |
| Baki Can Erdoğan | 230201052 | [@bakicanerdogan](https://github.com/bakicanerdogan) | Implementation Engineer | [Issue #2 (`DOC-02`)](https://github.com/seng321CoHobby/Co-Hobby/issues/2) |


---


## Detailed Member Contributions


### 1. Yıldırım Beyazıt Köroğlu
- **Student Number:** 230201076
- **GitHub Username:** `@beyazitKRGL`
- **Role & Responsibilities:** **Product Owner** — Responsible for problem definition, stakeholder identification and analysis, defining the intended project outcome, first-release scope vs. deferred features, and assumptions/risks analysis.
- **Completed Work in Sprint 1:**
  - Authored the Project Proposal (`docs/01-project-proposal.md`) including problem evidence, stakeholder analysis table, feasibility assessment, first-release scope, and the assumptions/risks matrix.
  - Documented the MIT open-source license selection rationale and collaborated on user story prioritization (`US-02`).
- **GitHub Traceability Links:**
  - **Issue:** [Issue #1 – `[DOC-01]` Draft Co-Hobby Project Proposal and Open-Source License Decision](https://github.com/seng321CoHobby/Co-Hobby/issues/1)
  - **Pull Request:** [PR #10](https://github.com/seng321CoHobby/Co-Hobby/pull/10)
  - **Commits:** [Commits by `@beyazitKRGL`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=beyazitKRGL)


---


### 2. Baki Can Erdoğan
- **Student Number:** 230201052
- **GitHub Username:** `@bakicanerdogan`
- **Role & Responsibilities:** **Implementation Engineer** — Responsible for defining the system vision, software responsibility boundaries, external service interactions, domain schema modeling, and story effort estimation.
- **Completed Work in Sprint 1:**
  - Authored the System Vision and Boundary specification (`docs/02-vision-and-boundary.md`).
  - Created the labeled Mermaid system context diagram illustrating interactions between Solo Hobbyists, Project Owners, the Co-Hobby Platform, Identity Provider, and External Media Hosts.
  - Defined system interface, security, and domain constraints and contributed to `US-01` profile schema design.
- **GitHub Traceability Links:**
  - **Issue:** [Issue #2 – `[DOC-02]` Define System Vision and Labeled System Boundary Diagram](https://github.com/seng321CoHobby/Co-Hobby/issues/2)
  - **Pull Request:** [PR #16](https://github.com/seng321CoHobby/Co-Hobby/pull/16) *(final merge to `develop`; earlier PRs #8 and #13 were superseded during branch cleanup)*
  - **Reviewed PRs:** [PR Reviews by `@bakicanerdogan`](https://github.com/seng321CoHobby/Co-Hobby/pulls?q=is%3Apr+reviewed-by%3Abakicanerdogan) *(PRs #11, #12, #14)*
  - **Commits:** [Commits by `@bakicanerdogan`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=bakicanerdogan)


---


### 3. Enes Alp Erkmen
- **Student Number:** 240201009
- **GitHub Username:** `@Bruhun`
- **Role & Responsibilities:** **Architect** — Accountable for the overall system architecture, API-first contract design (`api/openapi.yaml`), system boundary alignment, and technical review of pull requests.
- **Completed Work in Sprint 1:**
  - Designed and validated the standalone OpenAPI 3.1.0 specification (`api/openapi.yaml`) covering `/tags`, `/profiles`, `/groups`, `/groups/{groupId}/members`, `/projects`, `/projects/{projectId}/progress`, `/projects/{projectId}/share`, and `/feed/projects`.
  - Modeled reusable component schemas separating `memberRole` (`OWNER`/`MEMBER`) from `skillRole`, and defined RFC 9457 `Problem` responses (`400`, `401`, `403`, `404`, `409`).
  - Initialized the GitHub organization issue structure and conducted peer reviews across feature pull requests.
- **GitHub Traceability Links:**
  - **Issue:** [Issue #3 – `[API-01]` Design Valid OpenAPI 3.1.0 Contract Draft](https://github.com/seng321CoHobby/Co-Hobby/issues/3)
  - **Pull Request:** [PR #7](https://github.com/seng321CoHobby/Co-Hobby/pull/7) *(plus cleanup PR #12 to revert the accidental merge into `main`)*
  - **Reviewed PRs:** [PR Reviews by `@Bruhun`](https://github.com/seng321CoHobby/Co-Hobby/pulls?q=is%3Apr+reviewed-by%3ABruhun) *(PRs #8, #10, #13, #16)*
  - **Commits:** [Commits by `@Bruhun`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=Bruhun)


---


### 4. Mete Dugan
- **Student Number:** 240204029
- **GitHub Username:** `@xa1res`
- **Role & Responsibilities:** **Scrum Master** — Accountable for team role definitions, RACI responsibility governance, Git-Flow process compliance, and repository documentation organization.
- **Completed Work in Sprint 1:**
  - Authored the Team Roles and RACI Matrix document (`docs/03-roles-and-raci.md`) ensuring single accountability (`A`) per deliverable row.
  - Structured the root `README.md` with project overview, team roster, and direct navigation links to all Sprint 1 deliverables.
  - Contributed to backlog refinement (`US-07`) and pull request coordination.
- **GitHub Traceability Links:**
  - **Issue:** [Issue #4 – `[DOC-03]` Document Team Roles, RACI Matrix, and Submission README](https://github.com/seng321CoHobby/Co-Hobby/issues/4)
  - **Pull Request:** [PR #9](https://github.com/seng321CoHobby/Co-Hobby/pull/9)
  - **Reviewed PRs:** [PR Reviews by `@xa1res`](https://github.com/seng321CoHobby/Co-Hobby/pulls?q=is%3Apr+reviewed-by%3Axa1res) *(PR #15)*
  - **Commits:** [Commits by `@xa1res`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=xa1res)


---


### 5. Abdullah Şar
- **Student Number:** 240201019
- **GitHub Username:** `@sengProje64`
- **Role & Responsibilities:** **DevOps Engineer** — Responsible for GitHub repository rulesets, branch protection on `main` and `develop`, open-source license configuration, CI workflow setup, and release tagging.
- **Completed Work in Sprint 1:**
  - Authored the Lightweight Git-Flow Policy document (`docs/04-git-flow-policy.md`) and added the root MIT `LICENSE` file.
  - Configured GitHub branch protection rulesets preventing direct pushes/deletions on `main` and `develop` and enforcing pull request reviews.
  - Added automated OpenAPI validation workflow and managed the `sprint-1` release tag.
- **GitHub Traceability Links:**
  - **Issue:** [Issue #5 – `[OPS-01]` Establish Git-Flow Policy, LICENSE File, and OpenAPI CI Check](https://github.com/seng321CoHobby/Co-Hobby/issues/5)
  - **Pull Request:** [PR #15](https://github.com/seng321CoHobby/Co-Hobby/pull/15)
  - **Commits:** [Commits by `@sengProje64`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=sengProje64)


---


### 6. Hüseyin Yiğit Özkaya
- **Student Number:** 240201052
- **GitHub Username:** `@yigitozkaya07`
- **Role & Responsibilities:** **QA Engineer** — Accountable for the Initial Product Backlog, Definition of Ready (DoR), testable acceptance criteria, OpenAPI contract verification, and Sprint 1 submission evidence validation.
- **Completed Work in Sprint 1:**
  - Authored the Initial Product Backlog (`docs/05-product-backlog.md`) structured into Epics, Features, and 7 prioritized User Stories (`US-01`–`US-07`) with story point estimates, dependencies, and owners.
  - Completed the Sprint 1 Peer-Review exercise and assembled the master Sprint 1 report (`docs/seng_321_sprint_1_submission.md`) and `CONTRIBUTIONS.md`.
- **GitHub Traceability Links:**
  - **Issue:** [Issue #6 – `[DOC-04]` Create Prioritized Initial Product Backlog and Definition of Ready](https://github.com/seng321CoHobby/Co-Hobby/issues/6)
  - **Pull Request:** [PR #14](https://github.com/seng321CoHobby/Co-Hobby/pull/14)
  - **Reviewed PRs:** [PR Reviews by `@yigitozkaya07`](https://github.com/seng321CoHobby/Co-Hobby/pulls?q=is%3Apr+reviewed-by%3Ayigitozkaya07) *(PRs #7, #9)*
  - **Commits:** [Commits by `@yigitozkaya07`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=yigitozkaya07)

---


## Sprint 2 – Individual Contributions

- **Sprint:** 2 – Requirements & Architecture (milestone due 2026-11-24)
- **Sprint 2 Release Tag:** `sprint-2` — *placeholder until OPS-04 (#37) publishes the release: <https://github.com/seng321CoHobby/Co-Hobby/releases/tag/sprint-2>*
- **Submission Report:** [`docs/seng_321_sprint_2_submission.md`](docs/seng_321_sprint_2_submission.md)

Each Sprint 2 issue names one Responsible author and one Reviewer, plus any Contributors. The table lists what each member authored and reviewed; the sections below link the evidence.

| Name & Surname | GitHub Username | Project Role | Sprint 2 Issues (Responsible) | Authored PRs | Reviewed PRs |
|---|---|---|---|---|---|
| Yıldırım Beyazıt Köroğlu | [@beyazitKRGL](https://github.com/beyazitKRGL) | Product Owner | #26 | #42 | #44, #47 |
| Mete Dugan | [@xa1res](https://github.com/xa1res) | Scrum Master | #24, #36 | #49, #53 | #35 and #37 PRs (pending) |
| Enes Alp Erkmen | [@Bruhun](https://github.com/Bruhun) | Architect | #32, #33, #38 | #39, #41, #45, #46 | #40, #43, #44, #48, #49, #52 |
| Hüseyin Yiğit Özkaya | [@yigitozkaya07](https://github.com/yigitozkaya07) | QA Engineer | #27, #28, #35 | #43, #44 | #42, #51 |
| Abdullah Şar | [@sengProje64](https://github.com/sengProje64) | DevOps Engineer | #25, #29, #37 | #51, #52 | — |
| Baki Can Erdoğan | [@bakicanerdogan](https://github.com/bakicanerdogan) | Implementation Engineer | #30, #31, #34 | #40, #47, #48, #50 | #39, #41, #45, #46 |

*PRs #50 and #51 are open at the time of writing; #35, #36 and #37 are completed in the last step of the sprint.*


---


### Sprint 2 — Yıldırım Beyazıt Köroğlu
- **Role & Responsibilities:** **Product Owner** — owns the requirements and represents the product view in the UI/UX work.
- **Completed Work in Sprint 2:**
  - Authored the Software Requirements Specification (`docs/06-srs.md`): eight functional requirements with rationale and acceptance criteria, use cases UC-01 to UC-05 with alternate and error flows, data and interface requirements aligned with `api/openapi.yaml`, and the requirements traceability matrix.
  - Gave product input to the Figma prototypes and reviewed them against the SRS use cases (#30).
  - Reviewed the refined backlog against the contract and the SRS error flows (#27).
- **GitHub Traceability Links:**
  - **Issue:** [Issue #26 – `[SRS-01]` Write the Detailed Software Requirements Specification](https://github.com/seng321CoHobby/Co-Hobby/issues/26)
  - **Pull Request:** [PR #42](https://github.com/seng321CoHobby/Co-Hobby/pull/42)
  - **Reviewed PRs:** [PR #44](https://github.com/seng321CoHobby/Co-Hobby/pull/44), [PR #47](https://github.com/seng321CoHobby/Co-Hobby/pull/47)
  - **Commits:** [Commits by `@beyazitKRGL`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=beyazitKRGL)


---


### Sprint 2 — Baki Can Erdoğan
- **Role & Responsibilities:** **Implementation Engineer** — owns the UI/UX deliverable and the structural UML models that Sprint 3 implementation follows.
- **Completed Work in Sprint 2:**
  - Designed the eight high-fidelity Figma screens for US-01 to US-07, exported them as PNGs (`docs/figma/`), and mapped each screen to its story, use case, FR and API operations (`docs/09-ui-ux.md` §1–§2).
  - Drew the three user-flow diagrams in Figma, with the error branches from the contract (`docs/09-ui-ux.md` §3, `docs/diagrams/user-flow-*.png`).
  - Drew the UML class diagram and the sequence diagrams for `addGroupMember` and `updateProjectProgress` (`docs/diagrams/uml-class.*`, `uml-seq-*.*`).
  - Contributed to and reviewed the C4 container diagram and design decisions (#32).
- **GitHub Traceability Links:**
  - **Issues:** [Issue #30 – `[UX-01]`](https://github.com/seng321CoHobby/Co-Hobby/issues/30), [Issue #31 – `[UX-02]`](https://github.com/seng321CoHobby/Co-Hobby/issues/31), [Issue #34 – `[ARCH-03]`](https://github.com/seng321CoHobby/Co-Hobby/issues/34)
  - **Pull Requests:** [PR #40](https://github.com/seng321CoHobby/Co-Hobby/pull/40), [PR #47](https://github.com/seng321CoHobby/Co-Hobby/pull/47), [PR #48](https://github.com/seng321CoHobby/Co-Hobby/pull/48), [PR #50](https://github.com/seng321CoHobby/Co-Hobby/pull/50)
  - **Reviewed PRs:** [PR #39](https://github.com/seng321CoHobby/Co-Hobby/pull/39), [PR #41](https://github.com/seng321CoHobby/Co-Hobby/pull/41), [PR #45](https://github.com/seng321CoHobby/Co-Hobby/pull/45), [PR #46](https://github.com/seng321CoHobby/Co-Hobby/pull/46)
  - **Commits:** [Commits by `@bakicanerdogan`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=bakicanerdogan)


---


### Sprint 2 — Enes Alp Erkmen
- **Role & Responsibilities:** **Architect** — accountable for the architecture documentation and for keeping every document consistent with the API contract.
- **Completed Work in Sprint 2:**
  - Prepared the Sprint 2 document skeletons (`docs/06`–`09`, `docs/diagrams/README.md`) and drew the C4 Level 1 system context diagram (#38).
  - Authored `docs/08-architecture.md`: the C4 Level 2 container diagram, the architecture overview, and design decisions DD-01 to DD-04 linked to their NFRs.
  - Drew the UML use-case diagram and the milestone state diagram, and linked them from the SRS and the architecture document (#33).
  - Clarified the `403` response of `updateProjectProgress` as owner-only in `api/openapi.yaml` (PR #41).
  - Updated the repository description and topics (#25) and reviewed most Sprint 2 pull requests.
- **GitHub Traceability Links:**
  - **Issues:** [Issue #32 – `[ARCH-01]`](https://github.com/seng321CoHobby/Co-Hobby/issues/32), [Issue #33 – `[ARCH-02]`](https://github.com/seng321CoHobby/Co-Hobby/issues/33), [Issue #38 – `[DOC-08]`](https://github.com/seng321CoHobby/Co-Hobby/issues/38)
  - **Pull Requests:** [PR #39](https://github.com/seng321CoHobby/Co-Hobby/pull/39), [PR #41](https://github.com/seng321CoHobby/Co-Hobby/pull/41), [PR #45](https://github.com/seng321CoHobby/Co-Hobby/pull/45), [PR #46](https://github.com/seng321CoHobby/Co-Hobby/pull/46)
  - **Reviewed PRs:** [PR #40](https://github.com/seng321CoHobby/Co-Hobby/pull/40), [PR #43](https://github.com/seng321CoHobby/Co-Hobby/pull/43), [PR #44](https://github.com/seng321CoHobby/Co-Hobby/pull/44), [PR #48](https://github.com/seng321CoHobby/Co-Hobby/pull/48), [PR #49](https://github.com/seng321CoHobby/Co-Hobby/pull/49), [PR #52](https://github.com/seng321CoHobby/Co-Hobby/pull/52)
  - **Commits:** [Commits by `@Bruhun`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=Bruhun)


---


### Sprint 2 — Mete Dugan
- **Role & Responsibilities:** **Scrum Master** — accountable for Sprint 2 planning, the assessment checklist, the submission report, and reviews of the QA sweep and the release.
- **Completed Work in Sprint 2:**
  - Built the Sprint 2 assessment checklist (`docs/10-sprint-2-assessment-checklist.md`), since no official rubric was shared. It covers deliverables D1–D4, the submission requirements, process and consistency checks, the report structure, and a contribution-balance check.
  - Confirmed the Sprint 2 milestone and labels on all Sprint 2 issues (#24).
  - Assembled this Sprint 2 submission report (`docs/seng_321_sprint_2_submission.md`) and the Sprint 2 section of `CONTRIBUTIONS.md` (#36).
  - Reviewer of the final QA sweep (#35) and the Sprint 2 release (#37).
- **GitHub Traceability Links:**
  - **Issues:** [Issue #24 – `[PROC-01]`](https://github.com/seng321CoHobby/Co-Hobby/issues/24), [Issue #36 – `[DOC-07]`](https://github.com/seng321CoHobby/Co-Hobby/issues/36)
  - **Pull Requests:** [PR #49](https://github.com/seng321CoHobby/Co-Hobby/pull/49), [PR #53](https://github.com/seng321CoHobby/Co-Hobby/pull/53)
  - **Reviewed PRs:** #35 QA-sweep PR and #37 release PR (pending)
  - **Commits:** [Commits by `@xa1res`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=xa1res)


---


### Sprint 2 — Abdullah Şar
- **Role & Responsibilities:** **DevOps Engineer** — owns the verification tooling, the CI plan, repository hygiene, and the Sprint 2 release.
- **Completed Work in Sprint 2:**
  - Authored the quality-verification section of `docs/07-nfr-quality-measures.md` (§3): a verification tool, CI location and evidence for every NFR, the Sprint 3 CI plan, the demo-day load-test scenario, and the PR quality-gate checklist.
  - Removed the remaining demo template files (`index.html`, `package.json`) and recorded the clarification of the `@xekone1` commit author in `CONTRIBUTIONS.md` (#25).
  - Responsible for the Sprint 2 release: the `develop` → `main` release PR, the `sprint-2` tag and the GitHub Release (#37).
- **GitHub Traceability Links:**
  - **Issues:** [Issue #25 – `[OPS-03]`](https://github.com/seng321CoHobby/Co-Hobby/issues/25), [Issue #29 – `[NFR-02]`](https://github.com/seng321CoHobby/Co-Hobby/issues/29), [Issue #37 – `[OPS-04]`](https://github.com/seng321CoHobby/Co-Hobby/issues/37)
  - **Pull Requests:** [PR #51](https://github.com/seng321CoHobby/Co-Hobby/pull/51), [PR #52](https://github.com/seng321CoHobby/Co-Hobby/pull/52)
  - **Commits:** [Commits by `@sengProje64`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=sengProje64)


---


### Sprint 2 — Hüseyin Yiğit Özkaya
- **Role & Responsibilities:** **QA Engineer** — accountable for measurable quality targets, backlog readiness, and the final Sprint 2 QA sweep.
- **Completed Work in Sprint 2:**
  - Authored the NFR catalogue (`docs/07-nfr-quality-measures.md` §1–§2, §4): fourteen NFRs across performance, security, usability, reliability, maintainability and accessibility. Each has a measurable validation target and a verification method.
  - Refined the product backlog (`docs/05-product-backlog.md`): re-validated estimates (26 SP), acceptance criteria extended with the SRS error flows, the Definition of Done, the Sprint 3 implementation order, and scope control.
  - Contributed to and reviewed the SRS (#26); reviewed the verification-tooling section (#29).
  - Responsible for the final QA sweep and the Sprint 2 peer-review exercise (#35); contributor to and reviewer of the submission report (#36).
- **GitHub Traceability Links:**
  - **Issues:** [Issue #27 – `[DOC-06]`](https://github.com/seng321CoHobby/Co-Hobby/issues/27), [Issue #28 – `[NFR-01]`](https://github.com/seng321CoHobby/Co-Hobby/issues/28), [Issue #35 – `[QA-01]`](https://github.com/seng321CoHobby/Co-Hobby/issues/35)
  - **Pull Requests:** [PR #43](https://github.com/seng321CoHobby/Co-Hobby/pull/43), [PR #44](https://github.com/seng321CoHobby/Co-Hobby/pull/44)
  - **Reviewed PRs:** [PR #42](https://github.com/seng321CoHobby/Co-Hobby/pull/42), [PR #51](https://github.com/seng321CoHobby/Co-Hobby/pull/51)
  - **Commits:** [Commits by `@yigitozkaya07`](https://github.com/seng321CoHobby/Co-Hobby/commits/develop?author=yigitozkaya07)


---


## Note on Commit Author Identities

The commit history of `develop` contains two commits that GitHub attributes to the external account [`@xekone1`](https://github.com/xekone1) instead of a team member's account:

| Commit | Author recorded in Git | Message |
|---|---|---|
| [`bfe7a31`](https://github.com/seng321CoHobby/Co-Hobby/commit/bfe7a31) | `Baki Can <bakican30@outlook.com.tr>` | `docs: add system vision and boundary (Refs #2)` |
| [`64838a6`](https://github.com/seng321CoHobby/Co-Hobby/commit/64838a6) | `Baki Can <bakican30@outlook.com.tr>` | `docs: add system vision and boundary (Refs #2)` |

**Clarification:** both commits were authored by **Baki Can Erdoğan** (`@bakicanerdogan`) from a secondary e-mail address (`bakican30@outlook.com.tr`) that is linked to the GitHub account `@xekone1`. They belong to Baki Can Erdoğan's `DOC-02` work (Issue #2, PRs #8, #13 and #16) and are not contributions from anyone outside Team 19. All later commits by this member use the `@bakicanerdogan` account.
