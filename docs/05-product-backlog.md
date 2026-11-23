## Product backlog (Sprint 2 refinement)

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
Priorities and estimates (in story points, SP; total 26 SP) were re-validated in Sprint 2 for Sprint 3 readiness. Acceptance criteria are extended to match the SRS alternate/error flows in `docs/06-srs.md` and `api/openapi.yaml` (`application/problem+json` on `400`/`409` errors).

| Priority | ID | Feature | Story | Acceptance criteria | SP | Dependencies | Owner |
|---|---|---|---|---|---|---|---|
| 1 | US-01 | F-1.1 | As a hobbyist, I can view hobby tags and create a profile so that owners can evaluate my skills. | Public `GET /tags` returns `200` (invalid request returns `400`); valid `POST /profiles` returns `201`; missing fields or invalid `mediaUrls` return `400`; missing/invalid Bearer JWT returns `401`. | 3 | None | `@bakicanerdogan` |
| 2 | US-02 | F-2.1 | As a creator, I can create a group with my skill and open roles so that vacancies are clear. | Valid group returns `201` with creator as `OWNER`; missing fields or empty `neededRoles` return `400`; missing/invalid Bearer JWT returns `401`. | 3 | US-01 | `@beyazitKRGL` |
| 3 | US-03 | F-2.1 | As a hobbyist, I can search groups by category and role so that I can find a compatible team. | Public search returns `200` with matching groups or an empty list `[]`; missing/invalid `category` returns `400`. | 3 | US-02 | `@yigitozkaya07` |
| 4 | US-04 | F-2.2 | As a Project Owner, I can add a member to a specific open role so that the vacancy is filled. | Valid addition returns `200` and `MEMBER`; invalid payload/UUID returns `400`; missing/invalid JWT returns `401`; non-owner returns `403`; unknown group/user IDs return `404`; duplicate member or filled role returns `409` (`ROLE_SLOT_FULL`). | 5 | US-02, US-03 | `@Bruhun` |
| 5 | US-05 | F-3.1 | As a Project Owner, I can start a group project so that we can track its progress. | Valid project returns `201` in `PLANNING` (`isShared: false`); invalid payload/UUID returns `400`; missing/invalid JWT returns `401`; non-owner returns `403`; unknown group returns `404`. | 3 | US-04 | `@sengProje64` |
| 6 | US-06 | F-3.1 | As a Project Owner, I can advance stages sequentially so that progress remains structured. | Next sequential stage (`PLANNING -> WEEK_1 -> WEEK_2 -> COMPLETED`) returns `200`; invalid stage/UUID returns `400`; missing/invalid JWT returns `401`; non-owner returns `403`; unknown project returns `404`; skipped/backward stages return `409`. | 5 | US-05 | `@sengProje64` |
| 7 | US-07 | F-3.2 | As a Project Owner, I can share a completed project so that users can browse it in the public feed. | Sharing a `COMPLETED` project and public feed query return `200`; invalid feed request returns `400`; missing/invalid JWT on share returns `401`; non-owner returns `403`; unknown project returns `404`; sharing before `COMPLETED` returns `409`. | 4 | US-06 | `@xa1res` |

### Definition of Ready
- Actor, capability, and user value are explicit;
- Acceptance criteria cover the main success and alternate/failure cases in `docs/06-srs.md`;
- Dependencies and API operations in `api/openapi.yaml` are understood;
- The story fits within one sprint;
- Each story has a re-validated estimate and an assigned owner.

### Sprint 3 implementation order
Stories are sequenced by dependency order so core contracts and authentication unblock downstream work early in Sprint 3:

| Order | Story | Owner | Primary Focus | Unblocks |
|---:|---|---|---|---|
| 1 | `US-01` | `@bakicanerdogan` | Tags endpoint, profile creation, local JWT stub, and `Problem` error responses | `US-02` |
| 2 | `US-02` | `@beyazitKRGL` | Group creation with `OWNER` membership and open `neededRoles` | `US-03`, `US-04` |
| 3 | `US-03` | `@yigitozkaya07` | Public group discovery filtered by `category` and `seekingRole` | `US-04` |
| 4 | `US-04` | `@Bruhun` | Owner-only member assignment and duplicate/vacancy `409` guards | `US-05` |
| 5 | `US-05` | `@sengProje64` | Project initialization in `PLANNING` stage for an existing group | `US-06` |
| 6 | `US-06` | `@sengProje64` | Sequential milestone transitions (`PLANNING -> WEEK_1 -> WEEK_2 -> COMPLETED`) | `US-07` |
| 7 | `US-07` | `@xa1res` | Sharing `COMPLETED` projects and public shared-projects feed | End-to-end demo |

### Definition of Done (Sprint 3)
A Sprint 3 implementation story (`US-01`–`US-07`) is complete only when:
- Implemented endpoints, schemas, and status codes match `api/openapi.yaml` and the OpenAPI CI check passes;
- Automated unit and API integration tests cover both the main success flow and all specified error paths (`400`, `401`, `403`, `404`, `409` as applicable);
- Authentication (`BearerAuth`), `OWNER`-only authorization, and domain integrity rules are enforced in code;
- Code passes CI build, lint, and coverage targets referenced in `docs/07-nfr-quality-measures.md`;
- Changes are submitted via a `feature/*` branch and PR targeting `develop` with `Refs #N`, passing required checks and receiving at least one peer approval.

### Scope control
Sprint 2 backlog refinement introduces **no new features, stories, or endpoints** beyond the seven Sprint 1 stories (`US-01` through `US-07`). Deferred items from Sprint 1 (real-time chat, swipe matching, voice/video calls, payments, notifications, GPS tracking, moderation panels, raw media hosting, and building an external identity provider) remain out of scope for the first release.