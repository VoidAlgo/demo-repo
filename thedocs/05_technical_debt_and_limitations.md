# 05. Technical Debt, Limitations & Recommendations

## Current Limitations

1. **Incomplete HTML Document Structure**:
   - `index.html` consists only of a single header element (`<h1>...</h1>`).
   - It lacks proper HTML5 document structure (`<!DOCTYPE html>`, `<html>`, `<head>`, `<meta charset="utf-8">`, `<title>`, and `<body>`).
2. **Unused Declared Dependency**:
   - `@primer/css` is listed in `package.json`, but `index.html` does not import or link to any stylesheet from `@primer/css`.
3. **No Build or Serve Scripts**:
   - `package.json` contains no `"scripts"` block (e.g. `"test"`, `"build"`, or `"start"`).
4. **Hardcoded User Assignment**:
   - `.github/workflows/auto-assign.yml` assigns issues and PRs strictly to a single hardcoded username (`Makilesh`). If organization structure or active maintainers change, workflow runs will fail or misroute assignments.

## Technical Debt & Questionable Areas

1. **Action Version Pinning**:
   - `anishathalye/proof-html@v1.1.0` and `pozil/auto-assign-issue@v1` rely on older GitHub Action tags that may run on older Node runtime versions within GitHub Actions runners.
2. **Missing `.gitignore`**:
   - The repository currently lacks a `.gitignore` file. If a developer runs `npm install`, the `node_modules/` directory or package-lock files could inadvertently be committed to version control.
3. **Absence of Branch Protection Configuration**:
   - There are no repository-level rulesets or documentation regarding pull request review requirements or status check gating.

## Areas for Further Investigation

1. **GitHub Pages Deployment**:
   - Check if this repository is intended to be deployed via GitHub Pages (`Settings > Pages`), which would explain the static `index.html`.
2. **Primer CSS Integration**:
   - Clarify whether a bundler (Vite/Webpack) or direct stylesheet CDN link is intended for incorporating `@primer/css` styles into `index.html`.
3. **Repository Renaming Alignment**:
   - In branch `add-badges-to-readme`, badges link to `VoidAlgo/demo-repository` instead of `VoidAlgo/demo-repo`. Verify the canonical naming.
