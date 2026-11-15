# UI/UX Prototypes and User Flows

**Course:** BM321 Software Engineering
**Team:** 19
**Project:** Co-Hobby
**Sprint:** 2
**Status:** Draft — skeleton prepared by @Bruhun, authored by @bakicanerdogan (Issues #30, #31), product input @beyazitKRGL

> The UI/UX deliverable is the Figma project **including user-flow diagrams**.
> This document links the Figma file and commits exported PNGs so the artifacts survive
> independently of the Figma link. The Figma link must be **public view-only**.

## 1. Figma Project

- **Figma link (public view-only):** <TODO: paste the shared link here>
- **Figma workspace owner:** @bakicanerdogan
- **Product owner consulted:** @beyazitKRGL
- If the link is set to private/restricted, this deliverable cannot be graded.

## 2. Prototype Screens (Issue #30)

> Each screen must map to a use case in `docs/06-srs.md` and use the actual API fields
> (`displayName`, `bio`, `primaryCategory`, `skillRole`, `mediaUrls`, `neededRoles`, etc.),
> not invented data.

| # | Screen | Covers Story / Use Case | Figma Page | Exported PNG |
|---|---|---|---|---|
| 1 | Landing / Public Project Feed | US-07 / UC-05 | <TODO> | `docs/figma/01-feed.png` |
| 2 | Profile Creation | US-01 / UC-01 | <TODO> | `docs/figma/02-profile-creation.png` |
| 3 | Group Search Results (category + role filters) | US-03 / UC-03 | <TODO> | `docs/figma/03-group-search.png` |
| 4 | Group Detail with Open Roles / Vacancies | US-02 / UC-02 | <TODO> | `docs/figma/04-group-detail.png` |
| 5 | Owner Member-Assignment View | US-04 / UC-04 | <TODO> | `docs/figma/05-member-assignment.png` |
| 6 | Project Milestone Board (PLANNING → WEEK_1 → WEEK_2 → COMPLETED) | US-05, US-06 / UC-05 | <TODO> | `docs/figma/06-milestones.png` |
| 7 | Share Completed Project Dialog | US-07 / UC-05 | <TODO> | `docs/figma/07-share-project.png` |

> Add additional screens (e.g., sign-in, group creation form) below the table if needed.

## 3. User-Flow Diagrams (Issue #31)

> Draw the flows **inside Figma/FigJam** (as the assignment requires flows as part of the Figma
> deliverable), then export PNGs into `docs/diagrams/` and embed them here.
> Mark decision points and error branches (400, 403, 404, 409) on the flows.

### Flow 1 — Find a Group and Join (Hobbyist Journey)

<TODO: Figma frame/frame name, PNG path `docs/diagrams/user-flow-find-group.png`, and one-paragraph
narration of the journey (search → view → join an open role) including error branches.>

### Flow 2 — Create a Group and Fill Vacancies (Project Owner Journey)

<TODO: PNG path `docs/diagrams/user-flow-create-group.png`, narration of create → assign members →
roles filled, including 401/403/409 branches.>

### Flow 3 — Project Milestones and Sharing (Project Owner Journey)

<TODO: PNG path `docs/diagrams/user-flow-project-share.png`, narration of create project → advance
stages sequentially → share → public feed, including 409 when a stage is skipped or the project
is not COMPLETED.>

## 4. Traceability and Review

> A quick table for QA and the final submission report.

| Artifact | Linked Story / Use Case | Figma Page/Frame | Export Path | Reviewer |
|---|---|---|---|---|
| Prototype (all screens) | US-01 … US-07 / UC-01 … UC-05 | <TODO> | `docs/figma/` | @beyazitKRGL |
| Find-group flow | US-03 | <TODO> | `docs/diagrams/` | @yigitozkaya07 |
| Create-group flow | US-02, US-04 | <TODO> | `docs/diagrams/` | @yigitozkaya07 |
| Project-share flow | US-05, US-06, US-07 | <TODO> | `docs/diagrams/` | @yigitozkaya07 |
