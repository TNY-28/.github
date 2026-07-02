# .github

Global templates and working method for all my repos.

The issue and PR templates here apply automatically as defaults to
all my public repos that don't define their own.

## Contents

### Templates

- **Issue Templates** — Bug reports and feature requests (`ISSUE_TEMPLATE/`)
- **PR Template** — Checklist for pull requests (`PULL_REQUEST_TEMPLATE.md`)

### Workflow Templates

CI workflows ready to copy into any project:

- **ci-react.yml** — CI for React/Vite projects (install, build)
- **ci-django.yml** — CI for Django/Python projects (install, check, test)

#### How to use

Copy the workflow into the target project:

```bash
# From the project root
mkdir -p .github/workflows
cp path/to/template .github/workflows/ci.yml
```

Adjust as needed per project (env variables, Node/Python version, etc).

*(Automatic template suggestions in the Actions tab are an organization-only
GitHub feature — personal accounts always need the manual copy step above.)*

### Git Method

**git_method.md** — Personal Git and GitHub method.

Structure:
- FIXED rules (commits, push, config, AI policy) — don't change
- ADAPTABLE rules (branches, CI, testing, versioning) — decided per project
- Decision framework — questions to define what applies to each project
- Per-project decisions — format each project uses to log its choices

### Doc Model

**doc_model.md** — Documentation and execution model for any project,
with or without Git.

Structure:
- Two document natures: project docs (public, in Git) vs building
  docs (personal, gitignored)
- Standard project skeleton with a `building/` layer
- Naming conventions: identifiers in English, prose in Spanish
- Correction log that versions the model itself

### Other files
- `.gitignore` — OS and editor noise
- `LICENSE` — MIT

## Philosophy

- FIXED rules give confidence. ADAPTABLE rules give flexibility
- Templates and workflows are a starting point, not rigid rules
- Each project adjusts what it needs, documenting why
- If an adaptable rule repeats across every project, it gets promoted to fixed
