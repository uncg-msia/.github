# Contributing as a Student

You are welcome — and encouraged — to improve course materials.

Typos, broken links, unclear wording, notebook errors, and small fixes all
help the next person who works through the same content. Submitting a pull
request (PR) is a normal part of how we maintain these repositories. You do
not need special permission to propose a change; faculty review and merge
what looks good.

For cloning, everyday branch use, and environment setup, start with the
[organization profile README](profile/README.md).

## Access (outside collaborator)

Provide your **GitHub username** to your instructor as directed for the course.
You will be invited as an **outside collaborator** on the repositories you need;
accept the GitHub invitation before cloning or opening a PR. Full setup notes
are in the [organization profile README](profile/README.md#access-and-github-account).

## What students should contribute

**Preferred** contribution types (use the matching branch prefix):

| Type | Branch prefix | Examples of good work |
|:------|:---------------|:------------------------|
| Course submissions | `assignment/` | Work your instructor asked you to submit on a branch |
| Bug fixes | `bugfix/` | Broken notebook cell, wrong path, failing sample code |
| Documentation | `docs/` | Typos, unclear steps, broken links in READMEs/notes |
| Tests | `test/` | Missing or updated tests that match existing behavior |

Prefer **small, focused** PRs (one issue per PR when you can).

### Discuss with your instructor first

Do **not** open large or structural changes without talking to your instructor
(issue, email, or office hours). That includes:

- New features or new modules (`feature/`)
- Refactors that restructure code without fixing a bug (`refactor/`)
- Dependency upgrades or repo maintenance (`chore/`)
- Production hotfixes (`hotfix/`) — maintainers only
- Release branches (`release/`) — maintainers only
- Rewrites of lectures, rubrics, answer keys, or assignment redesigns

If you are unsure whether a change is appropriate, ask. A short issue describing
the problem is always welcome.

## Before you start

1. For day-to-day coursework, use the **most recent release tag** (`vYYYY.S.m`)
   unless your instructor asks you to work from **`main`**. Do **not** rely on
   **`develop`** for labs or exercises—it is work in progress and may not match
   stable materials. See the [organization profile README](profile/README.md)
   material hierarchy.
2. When proposing a materials fix, base your branch on **`develop`** when it
   exists (that is where maintainers land changes). For graded **assignment**
   branches, follow your instructor (often from the current release tag or
   `main`).
3. Check open issues and PRs so you do not duplicate someone else’s work.

## Branch naming convention

All branch names use a **type prefix**, then a short kebab-case description.

### Full prefix list (org standard)

| Prefix | Purpose | Examples |
|:--------|:---------|:----------|
| `feature/` | New functionality | `feature/add-dark-mode`, `feature/JIRA-456-user-authentication` |
| `bugfix/` | Fixing a known bug | `bugfix/login-redirect-loop`, `bugfix/null-pointer-on-checkout` |
| `hotfix/` | Urgent production fix | `hotfix/payment-gateway-timeout`, `hotfix/security-patch-xss` |
| `release/` | Preparing a release | `release/2026.1.1`, `release/2026-q1-launch` |
| `chore/` | Maintenance (not features/fixes) | `chore/update-dependencies`, `chore/migrate-to-node-20` |
| `refactor/` | Restructure without behavior change | `refactor/extract-auth-service` |
| `docs/` | Documentation only | `docs/update-api-reference`, `docs/add-contributing-guide` |
| `test/` | Adding or updating tests | `test/add-payment-integration-tests` |
| `assignment/` | **Course material submissions** | `assignment/smith-module-02` |

### Student prefixes (use these)

| Prefix | Format / notes |
|:--------|:----------------|
| `assignment/` | **`assignment/<lastname-module>`** — e.g. `assignment/smith-module-02`, `assignment/garcia-module-05` |
| `bugfix/` | `bugfix/<short-description>` — e.g. `bugfix/notebook-02-import-path` |
| `docs/` | `docs/<short-description>` — e.g. `docs/fix-typo-lecture-04` |
| `test/` | `test/<short-description>` — e.g. `test/add-week-3-smoke-tests` |

Avoid committing directly on `main` or `develop`. Always use your own branch.

## Create a branch and publish it

```bash
# From the branch your instructor names (main or develop)
git fetch origin
git checkout main    # or: git checkout develop
git pull

# Course submission
git checkout -b assignment/<lastname-module>
# e.g. git checkout -b assignment/smith-module-02

# Materials fix (pick one)
# git checkout -b bugfix/csv-path-week-2
# git checkout -b docs/clarify-container-setup
# git checkout -b test/add-module-01-assertions

# Make your changes, then commit
git add <files-you-changed>
git commit -m "Brief description of the change"

# Publish the branch
git push --set-upstream origin assignment/<lastname-module>
```

Equivalent longer form (create, then switch):

```bash
git branch assignment/<lastname-module>
git checkout assignment/<lastname-module>
```

## Open a pull request (for fixes and shared improvements)

After you publish a **bugfix**, **docs**, or **test** branch, open a PR so
maintainers can review it. Assignment branches may be reviewed differently
(follow your course’s submission instructions).

1. Prefer targeting **`develop`** for materials improvements. If the course only
   uses `main`, or your instructor says otherwise, follow their base branch.
2. On GitHub, after `git push`, use **Compare & pull request**, or the CLI:

   ```bash
   gh pr create --base develop --head bugfix/csv-path-week-2 \
     --title "bugfix: correct CSV path in week 2 notebook" \
     --body "What was wrong and what you changed."
   ```

### If you cannot push to the course repository

Fork the repo on GitHub, clone **your fork**, add the original repo as
`upstream`, branch and commit with the same naming rules, push to **your**
`origin`, then open a PR into upstream `develop` (or the branch your instructor
names):

```bash
git clone <your-fork-url>
cd <repository-name>
git remote add upstream <original-repository-url>

git fetch upstream
git checkout -b bugfix/csv-path-week-2 upstream/develop
# ... edit, commit ...
git push --set-upstream origin bugfix/csv-path-week-2
```

## Writing a helpful PR

In the PR description, briefly include:

1. **What** you changed
2. **Why** (what was wrong or unclear)
3. **How you checked** it (e.g. re-ran the notebook cell, re-read the section)

Example:

```text
Title: bugfix: correct CSV path in week 2 notebook

The load step pointed at data/raw/games.csv but the file is
data/games.csv. Updated the path and re-ran the cell successfully.
```

## After you open the PR

- A maintainer may request small changes — push more commits to the **same
  branch**; the PR updates automatically.
- Once merged, you can delete your branch.
- Material fixes usually land on `develop` first, then ship to students via a
  later **release tag** on `main`. Your fix may not appear in the latest
  student release the same day; that is expected.

## What not to do

- Do not change grading scales, rubrics, or private solution material
  unless an instructor asked you to.
- Do not ship refactors, features, or large cleanups without instructor buy-in.
- Do not force-push to `main` or `develop` (you wont be able to do this anyway)
- **Do not** commit secrets (API keys, passwords, personal tokens).

## Questions

If you are unsure whether a change is appropriate, open a GitHub **issue**
describing the problem, or ask your instructor. Opening a draft PR with a
question in the description is also fine.

Faculty and maintainers: see
[CONTRIBUTING_FACULTY.md](CONTRIBUTING_FACULTY.md) for release and tagging
workflows.
