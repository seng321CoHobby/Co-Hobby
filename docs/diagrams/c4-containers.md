# C4 Level 2 — Container Diagram (standalone source)

Canonical copy lives in `docs/08-architecture.md` §3.2. Keep this file in sync when the diagram changes.

```mermaid
---
title: Container diagram for Co-Hobby Platform (C4 Level 2)
---
flowchart TB
    hobbyist["<b>Solo Hobbyist</b><br/>[Person]<br/>Creates a profile, searches groups,<br/>browses the feed"]
    owner["<b>Project Owner</b><br/>[Person]<br/>Creates groups, assigns members,<br/>manages project milestones"]

    subgraph cohobby["Co-Hobby Platform [Software System]"]
        web["<b>Web Frontend</b><br/>[Container: single-page web app]<br/>Profile, group search, group detail,<br/>milestone board, and public feed screens"]
        api["<b>REST API</b><br/>[Container: Java, Spring Boot]<br/>Implements api/openapi.yaml under /api/v1;<br/>validates JWTs, enforces OWNER rules<br/>and sequential stages"]
        db[("<b>Database</b><br/>[Container: PostgreSQL]<br/>Tags, profiles, groups, members,<br/>projects, media URLs")]
    end

    auth["<b>Identity Provider</b><br/>[External System]<br/>External OAuth provider;<br/>local JWT stub in development"]
    media["<b>External Media Host</b><br/>[External System]<br/>Hosts portfolio media;<br/>platform stores URLs only"]

    hobbyist -- "Uses<br/>[HTTPS]" --> web
    owner -- "Uses<br/>[HTTPS]" --> web
    web -- "Signs in, obtains Bearer JWT<br/>[HTTPS / OAuth]" --> auth
    web -- "Calls API operations<br/>[HTTPS / JSON + Bearer JWT]" --> api
    api -- "Verifies JWT signature and claims<br/>[HTTPS]" --> auth
    api -- "Reads and writes<br/>[JDBC / SQL]" --> db
    web -. "Displays media from stored URLs<br/>[HTTPS]" .-> media

    classDef person fill:#08427b,stroke:#052e56,color:#ffffff
    classDef container fill:#438dd5,stroke:#2e6295,color:#ffffff
    classDef ext fill:#999999,stroke:#6b6b6b,color:#ffffff
    class hobbyist,owner person
    class web,api,db container
    class auth,media ext
    style cohobby fill:#ffffff,stroke:#444444,stroke-dasharray:5 5,color:#000000
```

PNG export: `c4-containers.png`, rendered from the block above with Mermaid (mermaid.live or mermaid-cli).
