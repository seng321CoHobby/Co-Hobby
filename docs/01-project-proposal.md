# Co-Hobby Project Proposal

| | |
|---|---|
| **Document** | `docs/01-project-proposal.md` (DOC-01, Issue #1) |
| **Owner** | [@beyazitKRGL](https://github.com/beyazitKRGL) |
| **Contributor** | [@bakicanerdogan](https://github.com/bakicanerdogan) |
| **Reviewer** | [@Bruhun](https://github.com/Bruhun) |

## 1. Purpose

This document defines the problem Co-Hobby addresses, its stakeholders, the intended outcome, the feasibility of the first release, the first-release scope, the assumptions and risks, and the open-source license decision.

Co-Hobby is a web platform where hobbyists build skill profiles, find open groups by hobby category and needed skill role, and then track and share the projects their groups complete. Group discovery and project follow-through are the two ideas the first release is built around.

## 2. Problem Statement

University students and local hobbyists usually look for collaborators on general-purpose platforms such as social networks, chat groups, and forums. These channels were not designed for this purpose, which causes several difficulties:

- **No structured filtering.** Users cannot search by hobby category and by the specific skill role a group needs (for example, a drummer for a music group).
- **Unclear vacancies.** A post rarely shows whether a group still has an open place for a given skill, so users spend time searching and messaging without knowing whether their skills are needed.
- **Information gets buried.** Group announcements are mixed with unrelated posts and disappear quickly.
- **No project follow-through.** Informal groups lose momentum because there is no simple way to track progress, and finished work is hard to showcase.

## 3. Stakeholders

| Stakeholder | Category | Needs and expectations | Influence or dependence |
|---|---|---|---|
| Solo hobbyists | Primary users | Create skill profiles, search groups by hobby category and needed role, and find active teams. | Depend on accurate profiles and vacancies. |
| Group creators / Project Owners | Primary users | Create groups, assign members to open roles, track milestones, and share finished projects. | Influence membership and project rules. |
| Project team (6 students) | Operational stakeholders | Deliver a working, documented first release within the sprint schedule; keep the scope consistent. | Own the delivery and the quality of the product. |
| Platform administrators | Operational stakeholders | Rely on predefined tags in the first release. Moderation tools are deferred. | Low first-release dependency. |
| Course evaluators | Sponsors and governance | Assess scope consistency, engineering evidence, and team workflow. | Authority over sprint assessment. |
| Identity provider | External provider | Supplies identity claims used to authenticate users. | Constrains the authentication interface. |
| External media hosts | External provider | Host portfolio media that profiles reference by URL. | Constrain what media can be shown. |

## 4. Intended Outcome

A registered hobbyist can filter open groups by category and needed role and be added to a compatible group in **less than three minutes** during a usability test.

After a group is formed, the Project Owner can track the project through sequential milestones (`PLANNING`, `WEEK_1`, `WEEK_2`, `COMPLETED`) and publish the completed project to the public feed through a single workflow.

## 5. Feasibility Assessment

### Technical

Feasible. The team plans a Spring Boot REST backend and a web frontend built against the OpenAPI contract (`api/openapi.yaml`). The domain is small: tags, profiles, groups, members, and projects. Portfolio media stays on external hosts, so the first release stores URLs only and does not process media files. The identity provider is not implemented by the team; a documented local JWT stub with the same API boundary is used during development.

### Schedule

Feasible if the scope stays controlled. The first release is limited to profiles, group formation, milestones, and project sharing. Chat, swipe matching, calls, payments, notifications, GPS, and administration tools are deferred. The backlog contains seven user stories (`US-01` to `US-07`) with story-point estimates, ordered by dependency.

### Operational

Feasible for a course-level release. Reading tags, searching groups, and browsing the project feed are public, while all write operations require an authenticated user. Restricted actions (assigning members, creating and advancing projects, sharing) are limited to the group's Project Owner. Because administration and moderation tools are deferred, the first release relies on predefined tags and owner control instead of moderation.

### Legal

Manageable. The system stores only a display name, a short bio, skill roles, and external media URLs, and processes no financial or medical data. Personal data is kept to the minimum needed, in line with KVKK/GDPR principles. Original project code is released under the MIT License (see section 9). Dependency licenses will be inspected for compatibility.

## 6. First-Release Scope

- **Predefined hobby categories and skill roles.** A fixed catalogue of categories and roles (for example, Music: Guitarist, Drummer, Vocalist) used by profiles and groups.
- **Hobbyist profiles with external media URLs.** A profile contains a display name, biography, primary category, skill role, and links to portfolio media hosted elsewhere.
- **Group creation and category/role search.** A creator opens a group with the roles it still needs. Anyone can search open groups by category and, optionally, by needed role.
- **Owner-controlled assignment to open skill roles.** Only the Project Owner adds a member to a specific open role. A duplicate member or an already filled role is rejected.
- **Sequential project milestones.** A group project moves only through `PLANNING → WEEK_1 → WEEK_2 → COMPLETED`; stages cannot be skipped or reversed.
- **Completed-project sharing and public feed.** Only completed projects can be shared, and shared projects appear in a public feed.

## 7. Deferred Features

The following are intentionally outside the first release:

- Real-time chat
- Swipe-based matching
- Voice and video calls
- Payments, selling services, and advertising
- Automated email or push notifications
- Live GPS tracking
- Administration and moderation panels
- Raw media hosting (media remains on external hosts)
- Implementation of an identity provider

## 8. Assumptions and Risks

| # | Type | Statement | Impact | Likelihood | Validation or response |
|---|---|---|---|---|---|
| 1 | Assumption | Users provide accurate profile and skill information. | Medium | Medium | Use required fields and predefined hobby and role tags. |
| 2 | Assumption | Owners and hobbyists agree on initial join interest outside the platform before an owner adds a member. | Medium | Medium | Check this workflow during peer review; consider join requests in a later release. |
| 3 | Assumption | Users can provide external URLs for portfolio media. | Low | Low | Validate URI formats and test with sample URLs. |
| 4 | Risk | A user is added twice or assigned to a role that is already filled. | Medium | Medium | Return `409 Conflict`; test duplicate and full-vacancy cases. |
| 5 | Risk | An owner skips project stages or shares an unfinished project. | Medium | Medium | Enforce sequential transitions and return `409 Conflict`. |
| 6 | Risk | The external identity provider is unavailable during development. | Medium | Medium | Use a documented local JWT stub with the same API boundary. |
| 7 | Risk | Public pages (groups, feed) show fake or inappropriate content, because moderation tools are deferred. | Medium | Medium | Require authentication for every write, limit sharing to completed projects, and plan moderation for a later release. |
| 8 | Risk | The scope grows beyond what the team can deliver in the sprint schedule. | High | Medium | Keep the deferred list explicit; the Product Owner prioritizes the backlog. |

## 9. License Decision

**Decision: MIT License for original project code.**

Rationale:

- It permits use, modification, distribution, and commercial or non-commercial reuse.
- It is short and permissive, and suitable for academic and community collaboration.
- It fits the team's goal of building an accessible hobby-collaboration platform.

Follow-up actions:

- Add the complete MIT license text as `LICENSE` in the repository root.
- Inspect the licenses of direct and transitive dependencies.
- Record incompatible or unknown licenses as release risks.

## 10. Consistency With Other Sprint 1 Artifacts

The first-release scope maps to the API contract and the initial backlog as follows:

| Scope item | API operation(s) | Backlog story |
|---|---|---|
| Hobby categories, skill roles, and profiles | `getTags`, `createProfile` | `US-01` |
| Group creation | `createGroup` | `US-02` |
| Group search by category and role | `listAvailableGroups` | `US-03` |
| Owner-controlled assignment to open roles | `addGroupMember` | `US-04` |
| Sequential project milestones | `createProject`, `updateProjectProgress` | `US-05`, `US-06` |
| Completed-project sharing and public feed | `shareProject`, `getSharedProjectsFeed` | `US-07` |
