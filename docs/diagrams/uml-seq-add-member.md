# UML Sequence — POST /groups/{groupId}/members (addGroupMember)

Owner assigns a member to an open skill role. Covers 400, 401, 403, 404, and 409 from
`api/openapi.yaml`.
PNG export: `uml-seq-add-member.png`.

```mermaid
sequenceDiagram
    actor PO as Project Owner
    participant API as Co-Hobby REST API
    participant DB as Database

    PO->>API: POST /groups/{groupId}/members<br/>{userId, skillRole}
    alt Missing or invalid bearer token
        API-->>PO: 401 Unauthorized
    else Authenticated
        API->>DB: find group by groupId
        alt Group not found
            DB-->>API: none
            API-->>PO: 404 Not Found
        else Group found
            DB-->>API: group (members, neededRoles)
            alt Requester is not the OWNER of the group
                API-->>PO: 403 Forbidden
            else Requester is OWNER
                alt Invalid payload (skillRole missing)
                    API-->>PO: 400 Bad Request (INVALID_INPUT)
                else Payload valid
                    API->>DB: find user by userId
                    alt User not found
                        DB-->>API: none
                        API-->>PO: 404 Not Found
                    else User found
                        alt userId already a member OR role vacancy full
                            API-->>PO: 409 Conflict (ROLE_SLOT_FULL)
                        else Vacancy open
                            API->>DB: insert GroupMember(userId, MEMBER, skillRole)
                            DB-->>API: saved group
                            API-->>PO: 200 OK GroupListingResponse
                        end
                    end
                end
            end
        end
    end
```

## Response mapping

| Status | Condition | OpenAPI |
|---|---|---|
| 200 | Member assigned, returns `GroupListingResponse` | `addGroupMember` `'200'` |
| 400 | Invalid payload | `BadRequest` |
| 401 | Missing/invalid auth | `'401'` |
| 403 | Caller is not the Project Owner | `'403'` |
| 404 | Group or user not found | `'404'` |
| 409 | Duplicate member or filled vacancy (`ROLE_SLOT_FULL`) | `'409'` |
