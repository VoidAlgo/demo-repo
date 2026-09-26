# 03. Configuration, Dependencies & Runtime

## Package Manifest (`package.json`)

The repository includes a minimal Node.js `package.json`:

```json
{
  "name": "demo-repo",
  "version": "0.2.0",
  "description": "A sample package.json",
  "dependencies": {
    "@primer/css": "17.0.1"
  },
  "license": "MIT"
}
```

### Dependencies Analysis

- `@primer/css: 17.0.1`:
  - Primer CSS is GitHub's open-source CSS framework.
  - In this repository, `@primer/css` is pinned at version `17.0.1`.
  - Note: The root `index.html` does not currently include a `<link>` tag referencing `@primer/css` directly from `node_modules` or a CDN, making this dependency a declared asset specification or design baseline for future build processes.

## Configuration & Secrets

- **Environment Variables**: None explicitly defined in repository `.env` files.
- **GitHub Secrets**:
  - `secrets.GITHUB_TOKEN`: Utilized by `.github/workflows/auto-assign.yml` to authenticate the assignment API call against GitHub's REST API. This token is automatically provisioned by GitHub Actions runners.
  - Job-level permissions are explicitly scoped (`issues: write`, `pull-requests: write`).

## Runtime & Execution Setup

### Prerequisites
- Node.js runtime (v16+ recommended)
- NPM or Yarn package manager

### Local Development Commands
1. Install dependencies:
   ```bash
   npm install
   ```
2. Serve locally (using any static HTTP server):
   ```bash
   npx serve .
   # or using Python 3
   python -m http.server 8000
   ```
3. Open browser:
   Navigate to `http://localhost:8000` or `http://localhost:3000` to view `index.html`.
