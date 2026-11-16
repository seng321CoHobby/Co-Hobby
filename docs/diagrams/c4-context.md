# C4 Level 1 — System Context Diagram (standalone source)

Canonical copy lives in `docs/08-architecture.md` §3.1. Keep this file in sync when the diagram changes.

```mermaid
C4Context
    title System Context diagram for Co-Hobby Platform
    Person(hobbyist, "Solo Hobbyist", "Finds groups by hobby category and open skill role; keeps a hobbyist profile")
    Person(owner, "Project Owner", "Creates groups, assigns members to open roles, tracks project milestones")
    System(System, "Co-Hobby Platform", "Hobby profiles, group discovery, sequential milestones, completed-project sharing")
    System_Ext(Auth, "Identity Provider", "External OAuth provider; a local JWT stub keeps the same boundary during development")
    System_Ext(Media, "External Media Host", "Hosts portfolio media; the platform stores URLs only")

    Rel(hobbyist, System, "Creates profile, searches groups, browses feed", "HTTPS / JSON")
    Rel(owner, System, "Creates groups, assigns members, manages projects", "HTTPS / JSON")
    Rel(System, Auth, "Verifies Bearer JWT", "HTTPS")
    Rel(Auth, System, "Returns validated identity claims", "HTTPS")
    Rel(hobbyist, Media, "Uploads portfolio media", "HTTPS")
    Rel(System, Media, "References media by stored URL (no runtime call)")
```

PNG export: `c4-context.png` — generate via <https://mermaid.live> (paste the block above, download PNG).
