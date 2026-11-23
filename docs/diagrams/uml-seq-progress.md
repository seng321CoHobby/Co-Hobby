# UML Sequence — PATCH /projects/{projectId}/progress (updateProjectProgress)

Advances a project milestone strictly sequentially: PLANNING → WEEK_1 → WEEK_2 → COMPLETED.
Skipped or backward stages return 409. Covers 400, 401, 403, 404, and 409 from `api/openapi.yaml`.
PNG export: `uml-seq-progress.png`.

```mermaid
sequenceDiagram
    actor PO as Project Owner
    participant API as Co-Hobby REST API
    participant DB as Database

    PO->>API: PATCH /projects/{projectId}/progress<br/>{progressStage}
    alt Missing or invalid bearer token
        API-->>PO: 401 Unauthorized
    else Authenticated
        API->>DB: find project by projectId
        alt Project not found
            DB-->>API: none
            API-->>PO: 404 Not Found
        else Project found
            DB-->>API: project (progressStage, group, group members)
            alt Requester is not the OWNER of the project's group
                API-->>PO: 403 Forbidden
            else Requester is OWNER
                alt progressStage not in enum or payload invalid
                    API-->>PO: 400 Bad Request (INVALID_INPUT)
                else Valid enum value
                    API->>API: is requested stage exactly the next stage after current?
                    alt Stage skipped or moved backward
                        API-->>PO: 409 Conflict (problem+json)
                    else Next sequential stage
                        API->>DB: update progressStage
                        DB-->>API: saved project
                        API-->>PO: 200 OK ProjectResponse
                    end
                end
            end
        end
    end
```

## Stage guard

| Current stage | Allowed next | Anything else |
|---|---|---|
| PLANNING | WEEK_1 | 409 |
| WEEK_1 | WEEK_2 | 409 |
| WEEK_2 | COMPLETED | 409 |
| COMPLETED | — (terminal) | 409 |

## Response mapping

| Status | Condition | OpenAPI |
|---|---|---|
| 200 | Stage advanced, returns `ProjectResponse` | `updateProjectProgress` `'200'` |
| 400 | Invalid payload | `BadRequest` |
| 401 | Missing/invalid auth | `'401'` |
| 403 | Caller is not the Project Owner | `'403'` |
| 404 | Project not found | `'404'` |
| 409 | Stage skipped or moved backward | `'409'` |

Note: the 403 follows the owner-only rule in `api/openapi.yaml` ("Only the Project Owner can advance
the project progress stage"), the same rule as US-06 and the other owner-only endpoints
(`addGroupMember`, `createProject`, `shareProject`).
