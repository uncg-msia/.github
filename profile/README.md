# UNCG ILRS - Information Library Research Sciences

## Introduction

Welcome to the UNCG ILRS (Information Library Research Sciences) organization!
This organization provides resources, tools, and documentation for students and
researchers involved in library and information sciences. Whether you're just
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

3. Check out `main` and fetch the latest course material for this semester:

   ```bash
   git checkout main && git fetch origin
   ```

4. Refer to that repository's `README.md` for course-specific setup. Course
   repositories either ship a `Containerfile` / `requirements.txt` (or
   equivalent) for the runtime environment, or are HTML-based modules.

### Branch Information

Each repository uses two primary branches:

- **main** — stable, production-ready course material. Use this branch for the
  most reliable content during the semester.
- **develop** — default branch where active development occurs. It may contain
  new material, experimental modules, or updates not yet finalized.

Generally these two branches stay in sync throughout the semester. If you need
to switch branches:

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

## Course Information and Summaries

- **IAN 604** — Machine Learning and Predictive Analytics
- **IAN 630** — Fundamentals of Health & Sport Informatics

## Contributing

Found a typo, broken notebook cell, or unclear step? Students are encouraged
to open a fix PR — see
[CONTRIBUTING_STUDENTS.md](https://github.com/uncg-msia/.github/blob/main/CONTRIBUTING_STUDENTS.md).

Faculty and maintainers (releases, tags, semester cutover):
[CONTRIBUTING_FACULTY.md](https://github.com/uncg-msia/.github/blob/main/CONTRIBUTING_FACULTY.md).

