# .github

Global templates and working method for all my repos.

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

**GIT_METHOD.md** — Personal Git and GitHub method.

Structure:
- FIXED rules (commits, push, config, AI policy) — don't change
- ADAPTABLE rules (branches, CI, testing, versioning) — decided per project
- Decision framework — questions to define what applies to each project
- Per-project decisions — log of what was decided and why

## Philosophy

- FIXED rules give confidence. ADAPTABLE rules give flexibility
- Templates and workflows are a starting point, not rigid rules
- Each project adjusts what it needs, documenting why
- If an adaptable rule repeats across every project, it gets promoted to fixed
