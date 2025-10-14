# Copilot Agent Onboarding Instructions

Welcome! These instructions give you all the context you need to make, build, test, and validate changes in the **p6m7g8-actions/cdk-construct-build** repository without extra searching.

---

## 1. Repository Summary
- This repo implements a **GitHub Action** composite step (`action.yml`) that builds and packages AWS CDK Constructs using JSII/pacmak.
- It provides:
  - A `ci:gha` build script (TypeScript compilation, linting).
  - A `jsii:pacmak:parallel` packaging step into multiple language targets.
  - GitHub workflows for PR validation, labeling, auto-approve, queuing, and releasing tags.

## 2. Tech Stack & Project Info
- **Languages**: TypeScript for the action, YAML for workflows.
- **Package Manager**: Yarn (v4 via Corepack).
- **Runtime**: Node.js (>=24; `.node-version`).
- **Tools**: AWS CDK, JSII, Pacmak, GitHub CLI (`gh`), semantic-release patterns.
- **Repo Size**: ~30 files, no large assets.

## 3. Build & Validation Steps
Always start from a clean clone.

1. Install dependencies  
   ```bash
   npm install --global corepack   # ensure compatible Yarn
   corepack enable
   yarn install --frozen-lockfile
   ```
2. Run CI build (compilation + lint)  
   ```bash
   yarn run ci:gha
   ```
3. Package JSII targets  
   ```bash
   yarn run jsii:pacmak:parallel
   ```
4. (Optional) Validate YAML  
   ```bash
   yamllint .github workflows action.yml
   ```
5. (Optional) Spellcheck  
   ```bash
   npx cspell "**/*.md" "**/*.yml"
   ```

Preconditions: always run `yarn install` and use Node version in `.node-version`.  
Postconditions: `dist/` contains `action.yml`, `releasetag.txt`, `changelog.md`.

## 4. Project Layout & Key Paths
```
/
├── action.yml
├── README.md
├── LICENSE
├── .vscode/settings.json
└── .github/
    ├── copilot-instructions.md   ← this file
    └── workflows/
        ├── pull-request-lint.yml
        ├── pr-labeler.yml
        ├── build.yml
        ├── auto-queue.yml
        ├── auto-approve.yml
        └── release.yml
```

- **action.yml**: composite action definition  
- **Workflows**: PR checks, labeling, merge queue, auto-approve, release.  
- **dist/**: generated on release (not checked in).  

## 5. Validation Pipelines
- **PR Title Lint** (`pull-request-lint.yml`): enforces conventional commits.  
- **Labeling & Approval** (`pr-labeler.yml`, `auto-approve.yml`).  
- **Merge Queue** (`auto-queue.yml`): enqueues successful PRs.  
- **Release** (`release.yml`): bumps version, generates changelog, creates GitHub release.

To replicate:
```bash
yarn install && yarn run ci:gha && yarn run jsii:pacmak:parallel
# For release simulation:
# git tag vX.Y.Z && git push
# gh workflow run release.yml --ref main
```

---

Trust these instructions and only search the repo if something here is missing or outdated. Good luck!
