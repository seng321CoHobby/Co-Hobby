## Initial backlog

### Backlog hierarchy
- **Epic 1: Hobbyist Identity**
  - Feature F-1.1: Tags and profiles (`US-01`).
- **Epic 2: Group Formation**
  - Feature F-2.1: Group creation and discovery (`US-02`, `US-03`).
  - Feature F-2.2: Role-based member assignment (`US-04`).
- **Epic 3: Project Execution and Showcase**
  - Feature F-3.1: Project milestones (`US-05`, `US-06`).
  - Feature F-3.2: Completed-project sharing (`US-07`).

### Prioritized user stories
Estimates are in story points (SP).

| Priority | ID | Feature | Story | Acceptance criteria | SP | Dependencies | Owner |
|---:|---|---|---|---|---:|---|---|
| 1 | US-01 | F-1.1 | As a hobbyist, I can view hobby tags and create a profile so that owners can evaluate my skills. | Tags return `200`; valid profile returns `201`; missing fields or invalid URLs return `400`. | 3 | None | `@bakicanerdogan` |
| 2 | US-02 | F-2.1 | As a creator, I can create a group with my skill and open roles so that vacancies are clear. | Valid group returns `201` with creator as `OWNER`; empty roles return `400`. | 3 | US-01 | `@beyazitKRGL` |
| 3 | US-03 | F-2.1 | As a hobbyist, I can search groups by category and role so that I can find a compatible team. | Matching groups or an empty list return `200`; missing category returns `400`. | 3 | US-02 | `@yigitozkaya07` |
| 4 | US-04 | F-2.2 | As a Project Owner, I can add a member to a specific open role so that the vacancy is filled. | Valid addition returns `200` and `MEMBER`; non-owner returns `403`; unknown IDs return `404`; duplicate/full role returns `409`. | 5 | US-02, US-03 | `@Bruhun` |
| 5 | US-05 | F-3.1 | As a Project Owner, I can start a group project so that we can track its progress. | Valid project returns `201` in `PLANNING`; non-owner returns `403`; unknown group returns `404`. | 3 | US-04 | `@sengProje64` |
| 6 | US-06 | F-3.1 | As a Project Owner, I can advance stages sequentially so that progress remains structured. | Next stage returns `200`; skipped/backward stages return `409`; unknown project returns `404`. | 5 | US-05 | `@sengProje64` |
| 7 | US-07 | F-3.2 | As a Project Owner, I can share a completed project so that users can browse it in the public feed. | Sharing and feed return `200`; sharing before `COMPLETED` returns `409`. | 4 | US-06 | `@xa1res` |

### Definition of Ready
- Actor, capability, and user value are explicit;
- Acceptance criteria cover the main success and failure cases;
- Dependencies and API operations are understood;
- The story fits within one sprint;
- Each story has an estimate and an owner.