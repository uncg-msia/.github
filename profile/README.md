# Information, Library, & Research Sciences (iLRS)

**University of North Carolina at Greensboro, School of Education**

## Introduction

Welcome to the iLRS (Information Library Research Sciences) page!
This organization provides resources, tools, and documentation for students, faculty, 
and collaborators involved in library and information sciences. Whether you're just
getting started or looking for advanced materials, this guide will help you
navigate the repositories effectively.

## Getting Started

You should find a single course repository for each semester/year. From year to
year, we publish new releases of course material using the format `YYYY.S.m`
where:

- **Major** (`YYYY`) — the calendar year
- **Minor** (`S`) — the semester (`1` = fall, `2` = spring)
- **Patch** (`m`) — starts at `1` and increments throughout the semester as needed

For example, `2026.1.1` is the initial release of course materials for fall 2026.
Git tags for those releases are prefixed with `v` (for example `v2026.1.1`).

### Material hierarchy (what to use)

Use the **most recent release** for day-to-day coursework unless your instructor
specifically asks you to work from a branch.

| Priority | What | Student use |
|:---------|:-----|:------------|
| **1 — default** | **Latest release tag** (`vYYYY.S.m`) | Stable materials and exercises for the term. Check out this tag (or download the GitHub Release). |
| **2 — only if told** | **`main`** | Use when the instructor asks you to work directly from `main`. It may sit between tagged releases. |
| **3 — not for routine work** | **`develop`** | Active development. Diffs and unfinished modules may appear here; content can change and may **not** include stable material or exercises yet. |

Prefer **tags over branches** for reading and completing labs. Treat anything on
`develop` as work in progress unless you are told otherwise.

### Access and GitHub account

Course repositories are typically **private**. To receive access:

1. Create a free [GitHub](https://github.com/) account if you do not already have
   one (use an address you check regularly; your institutional email is fine).
2. Send your **GitHub username** to your instructor (or as directed on Canvas /
   the syllabus) for each course that uses org repositories.
3. Faculty will add you as an **outside collaborator** on the repositories you
   need for that term. You will get a GitHub invitation email—**accept** it
   before cloning.

You only need collaborator access on the repos for your courses, not membership
in the whole organization. If a clone fails with “repository not found,” confirm
you accepted the invite and that you gave the instructor the correct username.

To get started with any UNCG ILRS repository:

1. Navigate to your preferred working directory and clone the repository:

   ```bash
   # For example...
   cd ~/coursework   # macOS / Linux
   cd ~\coursework   # PowerShell
   git clone <repository-url>
   ```

2. Enter the repository directory:

   ```bash
   cd <repository-name>
   ```

3. Fetch tags and check out the **latest release** for this semester (preferred):

   ```bash
   git fetch origin --tags
   # List recent release tags (highest first):
   git tag -l 'v*' --sort=-v:refname | head
   # Check out the most recent one for your term (example):
   git checkout v2026.1.1
   ```

   You can also open the repo on GitHub → **Releases** and use the newest
   `YYYY.S.m` release. Only if your instructor says so, use `main` instead:

   ```bash
   git fetch origin
   git checkout main
   git pull origin main
   ```

4. Refer to that repository's `README.md` for course-specific setup. Course
   repositories either ship a `Containerfile` / `requirements.txt` (or
   equivalent) for the runtime environment, or are HTML-based modules. If the
   repo includes `docs/ai-what-to-expect.md`, read that for AI-use defaults for
   the course.

### Branches and student work

Each repository also has long-lived branches:

- **`main`** — post-release line of student-facing content; use only when told
  (see hierarchy above).
- **`develop`** — default authoring branch. May contain experimental or incomplete
  material; not the default for graded labs or weekly exercises.

If you need to switch branches after checking out a tag:

```bash
git checkout <branch-name>
```

In some courses, you may be asked to create a feature branch to make changes or
submit work — or you may catch a bug or typo and want to fix it.

To create and publish a branch:

```bash
# Create and switch to your branch (longer form: git branch … then git checkout …)
git checkout -b <last-name/module-number>

# Make your changes and commit, then publish the branch:
git push --set-upstream origin <last-name/module-number>
```

Example branch names: `smith/module-02`, `garcia/module-05`. For a materials
fix, open a pull request after you push — see
[CONTRIBUTING_STUDENTS.md](https://github.com/uncg-msia/.github/blob/main/CONTRIBUTING_STUDENTS.md).

### Container Setup

Repositories that include a `Containerfile` do so for a reproducible
environment. Follow the individual repository docs when available; general
steps:

1. Install [Docker](https://docs.docker.com/get-docker/) or
   [Podman](https://podman.io/getting-started/installation).

2. Build the container:

   ```bash
   docker build -t <repo-name> .
   # or with Podman
   podman build -t <repo-name> .
   ```

3. Run the container:

   ```bash
   docker run -it --rm -v "$(pwd)":/app <repo-name>
   # or with Podman
   podman run -it --rm -v "$(pwd)":/app <repo-name>
   ```

## Using AI in coursework

AI tools may support learning in ILRS / MSIA courses. Your **syllabus and Canvas
for the term** always take priority if anything differs.

### Where to read the full guidance

1. **In your course repo (primary):** after you clone, look for
   `docs/ai-what-to-expect.md` and, when present, `docs/ai/` (workflow, privacy,
   disclosure, prompting, and related guides).
2. **Org student kit (canonical source for those guides):**
   [ai-kit-student](https://github.com/uncg-msia/ai-kit-student) — literacy
   handouts and optional learner-agent skills. Prefer the copies shipped in your
   course materials when both exist.

Optional local agent config (for example `AGENTS.md` or tool skill folders) is
**not required** unless your course says so. Browser chat tools are enough for
most work when they fit course rules.

### Org defaults (short)

- Prefer **attempt → assist → verify → own** before submitting.
- You own everything you submit and should be able to explain it.
- Do **not** put restricted data (PHI, credentialed extracts such as MIMIC,
  secrets, classmates’ work) into consumer AI tools.
- Disclose AI use when the course asks.

Questions about data or disclosure: ask your instructor or TA before the
deadline.

## Course Information and Summaries

The full course catalog for the MSIA program can be found [here](https://catalog.uncg.edu/courses/ian/)

## Contributing

Found a typo, broken notebook cell, or unclear step? Students are encouraged
to open a fix PR:
[CONTRIBUTING_STUDENTS.md](https://github.com/uncg-msia/.github/blob/main/CONTRIBUTING_STUDENTS.md).

Faculty and maintainers (releases, tags, semester cutover):
[CONTRIBUTING_FACULTY.md](https://github.com/uncg-msia/.github/blob/main/CONTRIBUTING_FACULTY.md).
