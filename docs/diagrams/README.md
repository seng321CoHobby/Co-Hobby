# Diagram Sources and Exports

All Sprint 2 architecture and user-flow diagrams are version-controlled here as **source files
and PNG exports**, so the artifacts survive independently of Figma, mermaid.live, or any other
external tool.

## Workflow

1. Write the diagram as a Mermaid block directly in the relevant markdown document
   (`docs/08-architecture.md`, `docs/06-srs.md`, `docs/09-ui-ux.md`) — GitHub renders it natively.
2. For the submission report and offline review, export a PNG:
   - Paste the Mermaid source into <https://mermaid.live> → Download PNG → save here.
   - Or export the PNG directly from Figma for the UI/UX diagrams.
3. Commit both the source and the PNG in the same PR so the source stays editable and the
   binary is reviewable in git history.

## Files

| Diagram | Source / Editor | Export File | Issue |
|---|---|---|---|
| C4 Level 1 — System Context | `docs/08-architecture.md` (Mermaid C4Context) | `c4-context.png` | #32 |
| C4 Level 2 — Containers | `docs/08-architecture.md` | `c4-containers.png` | #32 |
| UML Use-Case Diagram | `docs/diagrams/uml-use-case.md` | `uml-use-case.png` | #33 |
| UML Milestone State Diagram | `docs/diagrams/uml-state.md` | `uml-state.png` | #33 |
| UML Domain Class Diagram | `docs/diagrams/uml-class.md` | `uml-class.png` | #34 |
| UML Sequence — addGroupMember | `docs/diagrams/uml-seq-add-member.md` | `uml-seq-add-member.png` | #34 |
| UML Sequence — updateProjectProgress | `docs/diagrams/uml-seq-progress.md` | `uml-seq-progress.png` | #34 |
| User Flow — find & join group | Figma | `user-flow-find-group.png` | #31 |
| User Flow — create group & fill vacancies | Figma | `user-flow-create-group.png` | #31 |
| User Flow — milestones & sharing | Figma | `user-flow-project-share.png` | #31 |

## Notes

- Do not add npm tooling to this repository; Mermaid sources render on GitHub and PNG exports
  are produced with mermaid.live or Figma (no build step required).
- If a diagram changes, regenerate the PNG and commit both in the same PR so source and export
  stay in sync.
