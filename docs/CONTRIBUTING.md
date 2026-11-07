# Collaboration and GitHub workflow

1. Track deliverables in GitHub Issues. Suggested board: Backlog, Ready, In Progress, Review, Done.
2. Assign one owner per issue and another collaborator to review when practical.
3. Use feature branches (example: `feature/issue-5-feature-table`) and pull requests.
4. PRs should describe changes, verification steps, data assumptions, and relevant screenshots.
5. Use numbered notebooks for EDA and experiments; move reusable code into `src/`.
6. Never commit credentials, browser profiles, restricted raw data, or unlicensed exports.
7. Keep `main` stable and update docs when data contracts or modeling choices change.

## Definition of done
A task is complete only when its artifacts run or can be inspected, acceptance criteria are met, limitations are stated, and documentation is updated.

## Issue format
**Objective:** why the task matters.

**Checklist:** implementation steps.

**Acceptance criteria:** evidence a reviewer can verify.

**Dependencies:** prerequisite data or issues.
