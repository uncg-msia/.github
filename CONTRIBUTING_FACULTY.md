# Contributing as Faculty & Maintainers

This guide is for faculty and collaborators who maintain UNCG ILRS course
repositories.

- Student setup: [organization profile README](profile/README.md)
- Student pull requests: [CONTRIBUTING_STUDENTS.md](CONTRIBUTING_STUDENTS.md)

## Long-lived branches

| Branch | Role |
|:--------|:------|
| `develop` | Default branch. Day-to-day authoring and student fix PRs land here. |
| `main` | Stable, student-facing content for the current semester. |

Keep `develop` and `main` aligned during the semester once a release has
shipped. Prefer pull requests for anything that lands on `develop` or `main`
when branch protection is enabled.

## Branch naming convention

All short-lived branches use a **type prefix**, then a short kebab-case
description.

| Prefix | Purpose | Examples |
|:--------|:---------|:----------|
| `feature/` | New functionality | `feature/add-dark-mode`, `feature/JIRA-456-user-authentication` |
| `bugfix/` | Fixing a known bug | `bugfix/login-redirect-loop`, `bugfix/PROJ-789-null-pointer-on-checkout` |
| `hotfix/` | Urgent fix for production (`main`) | `hotfix/payment-gateway-timeout`, `hotfix/security-patch-xss` |
| `release/` | Preparing a release | `release/2026.1.1`, `release/2026-q1-launch` |
| `chore/` | Maintenance (not features/fixes) | `chore/update-dependencies`, `chore/migrate-to-node-20` |
| `refactor/` | Restructure without behavior change | `refactor/extract-auth-service`, `refactor/replace-redux-with-zustand` |
| `docs/` | Documentation only | `docs/update-api-reference`, `docs/add-contributing-guide` |
| `test/` | Adding or updating tests | `test/add-payment-integration-tests`, `test/increase-coverage-auth-module` |
| `assignment/` | Student course submissions | `assignment/smith-module-02`, `assignment/garcia-module-05` |

### Who uses which prefixes

| Audience | Typical prefixes |
|:----------|:------------------|
| **Students** | `assignment/`, `bugfix/`, `docs/`, `test/` only. Larger work (`feature/`, `refactor/`, `chore/`, etc.) should be discussed with the instructor first. |
| **Faculty / maintainers** | Full set above. `release/` and `hotfix/` are maintainer-owned. |

### Student assignment branches

Course material submissions use:

```text
assignment/<lastname-module>
```

Examples: `assignment/smith-module-02`, `assignment/nguyen-module-05-lab`.

Students create and publish with:

```bash
git checkout -b assignment/<lastname-module>
# ... make changes ...
git push --set-upstream origin assignment/<lastname-module>
```

Use assignment branches for graded, per-student work. For shared materials
improvements, ask students to open a PR into **`develop`** from `bugfix/`,
`docs/`, or `test/` branches (see [CONTRIBUTING_STUDENTS.md](CONTRIBUTING_STUDENTS.md)).

### Reviewing student PRs

When reviewing student PRs against **`develop`**:

1. Confirm the prefix matches the change (`bugfix` / `docs` / `test`) and the
   scope is small.
2. Confirm the change does not alter answer keys or private solutions
   unintentionally.
3. Redirect `feature/`, `refactor/`, or large rewrites to a conversation with
   the instructor if they were not pre-approved.
4. Request small follow-ups on the same branch when needed.
5. Merge into `develop`; ship to students on `main` via the release process
   below when you are ready.

### Hotfixes

`hotfix/` is for urgent corrections already on **`main`** (broken student-facing
material mid-semester). Prefer a tight PR into `main`, then merge back into
`develop`. Use sparingly; routine fixes should go `bugfix/` → `develop` →
`release/*` → `main`.

## Versioning

Releases use **`YYYY.S.m`** (Git tags are prefixed with `v`):

| Component | Meaning | Examples |
|:-----------|:---------|:----------|
| `YYYY` | Calendar year | `2026` |
| `S` | Semester: `1` = fall, `2` = spring | `1`, `2` |
| `m` | Patch within the semester (starts at `1`) | `1`, `2`, `10` |

Examples:

- `2026.1.1` / tag `v2026.1.1` — first fall 2026 materials release
- `2026.1.2` / tag `v2026.1.2` — mid-semester update
- `2027.2.1` / tag `v2027.2.1` — first spring 2027 release

Release branches follow the same scheme: `release/YYYY.S.m` (for example
`release/2026.1.1`).

## Day-to-day workflow

1. Clone the course repo and work from `develop`:

   ```bash
   git clone <repository-url>
   cd <repository-name>
   git checkout develop && git pull origin develop
   ```

2. Make changes on a prefixed topic branch (`feature/…`, `docs/…`, etc.), then
   open a PR into `develop`.

3. When materials are ready for students, cut a **release** (next section).

## Running a release

Each course repository should protect `develop` and `main` as appropriate.
Releases are cut from `develop` into `main` via a `release/*` branch. After the
PR merges, **CI creates the annotated tag and GitHub Release** (see
[Automated tagging](#automated-tagging)).

```bash
# 1. Ensure develop is up to date
git checkout develop
git pull origin develop

# 2. Create the release branch (name must match the version)
#    YYYY = year, S = semester (1 fall / 2 spring), m = patch
git checkout -b release/YYYY.S.m

# 3. Push the release branch
git push --set-upstream origin release/YYYY.S.m

# 4. Open a PR: release branch → main
gh pr create --base main --head release/YYYY.S.m \
  --title "Release YYYY.S.m" \
  --body "Semester release YYYY.S.m"

# 5. Review, then merge the PR into main
gh pr merge --merge
```

After the PR is merged:

1. CI validates the branch name, creates annotated tag `vYYYY.S.m`, and
   publishes a GitHub Release.
2. Fast-forward or merge `main` back into `develop` if they diverged (usually
   they should not):

   ```bash
   git checkout develop
   git pull origin develop
   git merge origin/main
   git push origin develop
   ```

3. Optionally delete the remote release branch after a successful release.

### Manual tagging (fallback)

If CI is unavailable or a course repo has not adopted the release workflow yet:

```bash
git checkout main
git pull origin main
git tag -a vYYYY.S.m -m "YYYY.S.m"
git push origin vYYYY.S.m
```

Prefer a single annotated tag (`git tag -a`); do not create both a lightweight
and an annotated tag for the same version.

## Automated tagging

    Course repositories can call the org reusable workflow:

[`create-release.yml`](.github/workflows/create-release.yml)

### What it does

| Trigger | Behavior |
|:---------|:----------|
| PR **merged** into `main` from `release/YYYY.S.m` | Creates annotated tag `vYYYY.S.m` (tag push then creates the Release) |
| Push of tag `vYYYY.S.m` | Creates a GitHub Release if one does not already exist |

Branch and tag names must match:

```text
release/2026.1.1  →  tag v2026.1.1  →  GitHub Release "2026.1.1"
```

### Wire it into a course repository

Add `.github/workflows/release.yml` in the course repo:

```yaml
name: Release

on:
  pull_request:
    types: [closed]
    branches: [main]
  push:
    tags:
      - "v*.*.*"

permissions:
  contents: write

jobs:
  release:
    uses: uncg-msia/.github/.github/workflows/create-release.yml@main
    secrets: inherit
```

Requirements:

- The course repo must allow GitHub Actions to create tags and releases
  (`contents: write`).
- Branch protection on `main` should still require review; the workflow only
  runs **after** a successful merge.
- Release branch names must match `release/YYYY.S.m` (digits only, as above).

## Checklist for a new semester

1. [ ] Confirm version scheme (`YYYY.1.1` for fall, `YYYY.2.1` for spring).
2. [ ] Land semester content on `develop`.
3. [ ] Cut `release/YYYY.S.1` → PR → `main`.
4. [ ] Confirm CI created tag `vYYYY.S.1` and the GitHub Release.
5. [ ] Point students at `main` (and the release notes / tag as needed).
6. [ ] Sync `develop` with `main` after the release.
