# 02. Architecture & CI/CD Workflows

## Architectural Overview

`demo-repo` implements a lightweight static web project model integrated directly with GitHub CI/CD automation.

```
+-------------------------------------------------------------+
|                         Repository                          |
|                                                             |
|   +-------------------+          +----------------------+   |
|   |    index.html     |          |     package.json     |   |
|   |  (Static Content) |          |  (@primer/css:17.0.1)|   |
|   +-------------------+          +----------------------+   |
+-------------------------------------------------------------+
                               |
               Triggered By GitHub Events
                               v
+-------------------------------------------------------------+
|                   GitHub Actions Workflows                  |
|                                                             |
|  +---------------------------+  +------------------------+  |
|  |     auto-assign.yml       |  |     proof-html.yml     |  |
|  | Events: issues / pr open  |  | Events: push, dispatch |  |
|  | Target: Makilesh          |  | Action: proof-html     |  |
|  | Uses: GITHUB_TOKEN        |  | Target: ./             |  |
|  +---------------------------+  +------------------------+  |
+-------------------------------------------------------------+
```

## Workflows Breakdown

### 1. Auto Assign (`.github/workflows/auto-assign.yml`)

- **Name**: `Auto Assign`
- **Triggers**:
  - `issues`: `[opened]`
  - `pull_request`: `[opened]`
- **Runner**: `ubuntu-latest`
- **Permissions**:
  - `issues: write`
  - `pull-requests: write`
- **Action Used**: `pozil/auto-assign-issue@v1`
- **Configuration**:
  - `repo-token`: `${{ secrets.GITHUB_TOKEN }}`
  - `assignees`: `Makilesh`
  - `numOfAssignee`: `1`
- **Operational Responsibility**: Ensures every newly filed issue and opened pull request is immediately assigned to maintainer `Makilesh` without manual triage intervention.

### 2. Proof HTML (`.github/workflows/proof-html.yml`)

- **Name**: `Proof HTML`
- **Triggers**:
  - `push` (all branches and commits pushed)
  - `workflow_dispatch` (manual trigger via GitHub UI/API)
- **Runner**: `ubuntu-latest`
- **Action Used**: `anishathalye/proof-html@v1.1.0`
- **Configuration**:
  - `directory: ./`
- **Operational Responsibility**: Scans HTML files in the repository directory (`./`) for structural integrity, broken hyperlinks, missing attributes (e.g., `alt` tags on images), and HTML syntax errors.
