# C4 Level 1 — System Context Diagram (standalone source)

Canonical copy lives in `docs/08-architecture.md` §3.1. Keep this file in sync when the diagram changes.

```mermaid
---
title: System Context diagram for Co-Hobby Platform (C4 Level 1)
---
flowchart TB
    hobbyist["<b>Solo Hobbyist</b><br/>[Person]<br/>Finds groups by hobby category and<br/>open skill role; keeps a hobbyist profile"]
    owner["<b>Project Owner</b><br/>[Person]<br/>Creates groups, assigns members to<br/>open roles, tracks project milestones"]
    system["<b>Co-Hobby Platform</b><br/>[Software System]<br/>Hobby profiles, group discovery,<br/>sequential milestones, completed-project sharing"]
    auth["<b>Identity Provider</b><br/>[External System]<br/>External OAuth provider; a local JWT stub<br/>keeps the same boundary during development"]
    media["<b>External Media Host</b><br/>[External System]<br/>Hosts portfolio media;<br/>the platform stores URLs only"]

    hobbyist -- "Creates profile, searches groups,<br/>browses feed<br/>[HTTPS / JSON]" --> system
    owner -- "Creates groups, assigns members,<br/>manages projects<br/>[HTTPS / JSON]" --> system
    system -- "Verifies Bearer JWT<br/>[HTTPS]" --> auth
    auth -- "Returns validated identity claims<br/>[HTTPS]" --> system
    hobbyist -- "Uploads portfolio media<br/>[HTTPS]" --> media
    system -. "References media by stored URL<br/>(no runtime call)" .-> media

    classDef person fill:#08427b,stroke:#052e56,color:#ffffff
    classDef sys fill:#1168bd,stroke:#0b4884,color:#ffffff
    classDef ext fill:#999999,stroke:#6b6b6b,color:#ffffff
    class hobbyist,owner person
    class system sys
    class auth,media ext
```

PNG export: `c4-context.png`, rendered from the block above with Mermaid (mermaid.live or mermaid-cli).
