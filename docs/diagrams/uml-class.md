# UML Domain Class Diagram

Source of truth: `api/openapi.yaml` component schemas. Every attribute below maps to an
OpenAPI property. PNG export: `uml-class.png`.

```mermaid
classDiagram
    direction LR

    class TagCategory {
        +String category
        +String[] roles
    }

    class NewProfile {
        +String displayName
        +String bio
        +String primaryCategory
        +String skillRole
        +URI[] mediaUrls
    }

    class ProfileResponse {
        +UUID id
        +UUID userId
    }

    class NewGroupListing {
        +String groupName
        +String description
        +String category
        +String creatorSkillRole
        +String[] neededRoles
    }

    class GroupListingResponse {
        +UUID id
        +GroupMember[] members
    }

    class GroupMember {
        +UUID userId
        +MemberRole memberRole
        +String skillRole
    }

    class AddMemberRequest {
        +UUID userId
        +String skillRole
    }

    class NewProject {
        +UUID groupId
        +String title
        +String description
    }

    class ProjectResponse {
        +UUID id
        +ProgressStage progressStage
        +Boolean isShared
    }

    class ProgressUpdateRequest {
        +ProgressStage progressStage
    }

    class Problem {
        +String title
        +Integer status
        +String code
        +String detail
    }

    class MemberRole {
        <<enumeration>>
        OWNER
        MEMBER
    }

    class ProgressStage {
        <<enumeration>>
        PLANNING
        WEEK_1
        WEEK_2
        COMPLETED
    }

    ProfileResponse --|> NewProfile : allOf
    GroupListingResponse --|> NewGroupListing : allOf
    ProjectResponse --|> NewProject : allOf
    GroupListingResponse "1" *-- "0..*" GroupMember : members
    GroupMember --> MemberRole : memberRole
    ProjectResponse --> ProgressStage : progressStage
    ProgressUpdateRequest --> ProgressStage : progressStage
    NewProject "1" --> "1" GroupListingResponse : groupId references
    NewProfile ..> TagCategory : primaryCategory
    AddMemberRequest ..> GroupMember : creates
```

## Attribute cross-check

| Class | Attributes | OpenAPI schema |
|---|---|---|
| NewProfile | displayName, bio, primaryCategory, skillRole, mediaUrls | `NewProfile` |
| ProfileResponse | id, userId (+ NewProfile) | `ProfileResponse` |
| NewGroupListing | groupName, description, category, creatorSkillRole, neededRoles | `NewGroupListing` |
| GroupListingResponse | id, members (+ NewGroupListing) | `GroupListingResponse` |
| GroupMember | userId, memberRole, skillRole | `GroupMember` |
| AddMemberRequest | userId, skillRole | `AddMemberRequest` |
| NewProject | groupId, title, description | `NewProject` |
| ProjectResponse | id, progressStage, isShared (+ NewProject) | `ProjectResponse` |
| ProgressUpdateRequest | progressStage | `ProgressUpdateRequest` |
| Problem | title, status, code, detail | `Problem` |
| TagCategory | category, roles | `TagCategory` |

Note: `ProfileResponse`, `GroupListingResponse`, and `ProjectResponse` inherit their base
attributes through `allOf`; the diagram shows this as generalization instead of repeating them.
