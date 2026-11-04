# SENG 321 – Sprint 1 Individual Contributions (CONTRIBUTIONS.md)

- **Project Name:** Co-Hobby
- **Team Number:** 19
- **GitHub Repository:** https://github.com/seng321CoHobby/Co-Hobby
- **Sprint 1 Release Tag:** [`sprint-1`](https://github.com/seng321CoHobby/Co-Hobby/releases/tag/sprint-1)


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