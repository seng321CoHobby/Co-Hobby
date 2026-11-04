# Git-Flow Branching Policy & Conventions

## Branch Roles
- **main**: Production-ready stable code. Direct pushes are blocked.
- **develop**: Integration branch for features. Direct pushes are blocked.
- **feature/<issue>-<short-name>**: Feature branches branched from `develop` and merged back into `develop` via PR.
- **release/***: Branch created for preparing a new production release.
- **hotfix/***: Critical fixes branched from `main` and merged into both `main` and `develop`.

## PR Review Rules
- Every Pull Request requires at least one approval from an accountable reviewer.
- All automated status checks (e.g., OpenAPI linting) must pass before merging.
- Direct pushes and unreviewed merges are strictly prohibited.

## Commit Traceability Conventions
- Commits must follow Conventional Commits standard (e.g., `feat:`, `fix:`, `docs:`, `chore:`).
- Commit messages should reference the related issue ID where applicable.