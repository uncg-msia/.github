# UNCG MSIA

**M.S. in Informatics and Analytics** — [program page](https://www.uncg.edu/degrees/informatics-and-analytics-m-s/)  
Department of Information, Library, and Research Sciences (iLRS), School of Education, UNC Greensboro.

This organization holds **private course materials** and staff handbooks. Canvas is where graded work is submitted.

## Access

**Staff and students are not added the same way.**

| Who | How you get in | What you can see |
|:----|:---------------|:-----------------|
| Faculty | Org invite, then the `faculty` team | Master course repos, term repos, [msia-faculty](https://github.com/uncg-msia/msia-faculty), [msia-ta](https://github.com/uncg-msia/msia-ta) |
| Teaching assistants | Org invite, then `teaching-assistants` | Assigned **term** repos + [msia-ta](https://github.com/uncg-msia/msia-ta). Not the faculty handbook. |
| Students | **Outside collaborator** on that term’s course repo only | That one repository (for example `ian-630-2026.1`). Not this org profile, not master repos, not staff handbooks. |

Org default permission is **none**. An org invite still opens nothing until a **team** is assigned. That path is for staff.

Students are **not** org members. They get a repository invitation for the **term offering** (`ian-630-2026.1`, not `ian-630`). After the term, collaborators are removed and the term repo is archived so the next offering starts clean.

If you cannot see a repository you expect — or you can see one you should not — reach out. Students: your **instructor**. Staff team mistakes: an **org admin**.

## Students

Your front door is the **term repository README** your instructor links (Canvas / syllabus). You will not see this organization page; that is expected.

1. Create a free [GitHub](https://github.com/) account if you do not have one (use an address you check regularly; your UNCG email is fine).
2. Send your **GitHub username** to your instructor as directed on Canvas / the syllabus.
3. Accept the **repository** invitation for this term’s course (email or GitHub notifications). You are not joining the whole organization.
4. If a clone fails with “repository not found,” you have not accepted that invite, or the username you sent was wrong.

### What to check out

Use the **most recent release** for day-to-day coursework unless your instructor asks you to work from a branch.

| Priority | What | Student use |
|:---------|:-----|:------------|
| **1 — default** | **Latest release tag** (`vYYYY.S.m`) | Stable materials and exercises for the term |
| **2 — only if told** | **`main`** | Between tagged releases, when the instructor says so |
| **3 — not for routine work** | **`develop`** | Authoring branch. May be incomplete; not the default for labs |

`YYYY` is the calendar year, `S` is the semester (`1` = fall, `2` = spring), `m` starts at `1` and increments during the term. Example: `2026.1.1` / tag `v2026.1.1` is the first fall 2026 materials release.

```bash
cd ~/coursework          # macOS / Linux
# cd ~\coursework        # PowerShell
git clone <repository-url>
cd <repository-name>

git fetch origin --tags
git tag -l 'v*' --sort=-v:refname | head
git checkout v2026.1.1   # use the tag your instructor names
```

You can also open the repo on GitHub → **Releases** and use the newest `YYYY.S.m` release.

Then follow **that repository’s `README.md`** for course-specific setup.

### Environment

Courses that ship a `Containerfile` expect [Docker](https://docs.docker.com/get-docker/) or [Podman](https://podman.io/getting-started/installation). Some also support a local `uv` install. Use the course README; this is only the generic container shape:

```bash
docker build -t <repo-name> .
docker run -it --rm -v "$(pwd)":/app -w /app <repo-name>
# or: podman build / podman run with the same flags
```

### AI in coursework

Syllabus and Canvas for the term win if anything conflicts.

- **Default:** read `docs/ai-what-to-expect.md` in the course repo (and `docs/ai/` when present). You do **not** install a kit.
- **Optional:** use a local learner agent only if **that course’s README** says to.
- Prefer **attempt → assist → verify → own**. You own what you submit.
- Do **not** put restricted data (PHI, credentialed extracts such as MIMIC, secrets, classmates’ work) into consumer AI tools.
- Disclose AI use when the course asks.

### Student work and fixes

Long-lived branches: `main` (student-facing after a release) and `develop` (authoring). For a graded branch or a small materials fix, use the prefixes in
[CONTRIBUTING_STUDENTS.md](https://github.com/uncg-msia/.github/blob/main/CONTRIBUTING_STUDENTS.md)
(for example `assignment/smith-module-02`, `bugfix/…`, `docs/…`).

## Faculty

Confirm you are on the **`faculty`** team. How-tos live in the private handbook — not here:

**[msia-faculty](https://github.com/uncg-msia/msia-faculty)** — access, term offerings, [symkit](https://github.com/csymd/symkit) install, new masters, releases.

Teaser (full notes in the handbook; requires a Rust toolchain today):

```bash
# from a clone of csymd/symkit
./cli/symkit install /path/to/course --harness teaching --role instructor
```

Commit student-safe `docs/`. Do not commit staff packs or `.agents/` / `.grok/` to a student-visible branch.

## Teaching assistants

Confirm you are on **`teaching-assistants`**. How-tos live in:

**[msia-ta](https://github.com/uncg-msia/msia-ta)** — TA-role install, reviewing student PRs, evaluation norms, boundaries.

Install **`--role ta` only**. You will not see `msia-faculty`; that is expected. Do not install instructor packs.

## Courses

Each catalog course has a **master** repo (faculty only) and a **term** repo (what students are invited to).

| Course | Title | Master (staff) | Term offering (students) |
|:-------|:------|:---------------|:-------------------------|
| IAN 604 | Machine Learning and Predictive Analytics | `ian-604` | `ian-604-2026.1` |
| IAN 630 | Fundamentals of Health Informatics | `ian-630` | `ian-630-2026.1` |

Program catalog: [IAN courses](https://catalog.uncg.edu/courses/ian/).

Some **term** repos also publish a study hub on GitHub Pages (reading / self-check only). Graded work stays on Canvas. The term README names the URL when it exists.

## Contributing

- Students: [CONTRIBUTING_STUDENTS.md](https://github.com/uncg-msia/.github/blob/main/CONTRIBUTING_STUDENTS.md)
- Faculty (releases and semester cutover): [msia-faculty](https://github.com/uncg-msia/msia-faculty) — a short pointer remains in [CONTRIBUTING_FACULTY.md](https://github.com/uncg-msia/.github/blob/main/CONTRIBUTING_FACULTY.md)
- Teaching assistants: [msia-ta](https://github.com/uncg-msia/msia-ta)
