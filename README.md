# .github

Global templates and working method for all my repos.

The issue and PR templates here apply automatically as defaults to
all my repos that don't define their own.

## Contents

### Templates

- **Issue Templates** (`ISSUE_TEMPLATE/`) - Feature, task, bug, decision
  (ADR) and epic. Each one asks for a "Done when" condition
- **Issue template config** (`ISSUE_TEMPLATE/config.yml`) - Turns off blank
  issues, so every issue starts from a template
- **PR Template** (`PULL_REQUEST_TEMPLATE.md`) - Summary, linked issue, what
  changed, decisions, how it was tested, done criteria and a checklist

The templates add the labels `feat`, `fix`, `chore`, `decision` and `epic`.
GitHub only applies a label that already exists in the repo, so each repo
creates them first.

### Workflow Templates

CI workflows ready to copy into any project:

- **ci-react.yml** - CI for React/Vite projects (install, build)
- **ci-django.yml** - CI for Django/Python projects (install, check, test)

#### How to use

Copy the workflow into the target project:

```bash
# From the project root
mkdir -p .github/workflows
cp path/to/template .github/workflows/ci.yml
```

Adjust as needed per project (env variables, Node/Python version, etc).

*(Automatic template suggestions in the Actions tab are an organization-only
GitHub feature - personal accounts always need the manual copy step above.)*

### Git Method

**git_method.md** - Personal Git and GitHub method.

Structure:
- FIXED rules (commits, push, config, AI policy) - don't change
- ADAPTABLE rules (branches, merge, CI, testing, versioning, issues and
  labels) - decided per project
- Group repos - what gets configured: branch ruleset, a single merge method,
  labels, CODEOWNERS and a project board with Status only
- PR reviews - a verdict and numbered findings, each one marked by whether
  it blocks the merge
- Decision framework - questions to define what applies to each project
- Per-project decisions - format each project uses to log its choices

### Doc Method

**doc_method.md** - Documentation and execution model for any project,
with or without Git.

Structure:
- Two document natures: project docs (public, in Git) vs building
  docs (personal, gitignored)
- Standard project skeleton with a `building/` layer
- Content rules: who owns each fact, references with URL and how they
  were consulted, explicit design principles
- Diagram conventions: each diagram answers a specific reader, one
  notation per view (C4, UML, crow's foot ER), legends checked by drawing
- Decisions go to the logs when they are made, not at the end
- Naming conventions: identifiers in English, prose in Spanish
- Correction log that versions the model itself

### Other files
- `.gitignore` - OS and editor noise
- `LICENSE` - MIT

## Philosophy

- FIXED rules give confidence. ADAPTABLE rules give flexibility
- Templates and workflows are a starting point, not rigid rules
- Each project adjusts what it needs, documenting why
- If an adaptable rule repeats across every project, it gets promoted to fixed
