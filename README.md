# ds-project-layout: a Claude Code skill for data-science repositories

A [Claude Code](https://code.claude.com/docs) skill that keeps data-science and ML
repositories in the [Cookiecutter Data Science v2](https://cookiecutter-data-science.drivendata.org/)
layout. Claude reads it before creating a project, adding a file or moving code. New work
then lands in predictable places: features in the module, each model family under
`modeling/`, one-off investigations under `analysis/`, and data and checkpoints out of git.
No more `dcn/`, `final_v2/` and `try_this/` folders piling up at the repo root.

## What it covers

- **The target layout:** `data/{raw,external,interim,processed}`, `models/`, `notebooks/`,
  `references/`, `reports/`, and an importable module with `config.py`, `dataset.py`,
  `features.py` and `modeling/`.
- **A "where does this file go?" table** for features, new model types, data loading,
  constants, one-off analyses, figures, checkpoints and logs.
- **Rules for every change:**
  - no new top-level folders
  - artifacts gitignored
  - paths defined once in `config.py`
  - no `sys.path` patches
  - thin entry points
  - traceable results
  - no secrets in git
- **Safe migration of existing repos:** move files gradually, never under a running job,
  using `git mv`, fixing every old path and smoke-testing afterwards.
- **A short checklist** Claude runs before finishing a change.

The skill itself is [SKILL.md](plugins/ds-project-layout/skills/ds-project-layout/SKILL.md).

## Install

### As a plugin (recommended)

```bash
claude plugin marketplace add shashankg7/claude-ds-project-layout
claude plugin install ds-project-layout@ds-project-layout
```

Inside a Claude Code session, the equivalents are `/plugin marketplace add ...` and
`/plugin install ...`.

### As a plain skill

Copy the skill folder into your personal skills (applies to all projects):

```bash
git clone https://github.com/shashankg7/claude-ds-project-layout
mkdir -p ~/.claude/skills
cp -r claude-ds-project-layout/plugins/ds-project-layout/skills/ds-project-layout ~/.claude/skills/
```

To apply it to one repository and share it with collaborators, copy it to `.claude/skills/`
in that repository instead.

### Make it a standing rule (optional)

Claude loads a skill when its description matches the task. To have the layout applied to
every change, add this to `~/.claude/CLAUDE.md` (all projects) or to a project's `CLAUDE.md`:

```markdown
## Repository layout
Follow the `ds-project-layout` skill for every new project and every code change.
Read it before creating a project, adding a file or folder, or moving code.
```

## Precedence

The skill defers to a project's own documented conventions (README, CLAUDE.md, AGENTS.md,
CONTRIBUTING). Use it as the default where a project has none.

## Credits

The layout follows [Cookiecutter Data Science](https://github.com/drivendata/cookiecutter-data-science)
by DrivenData (MIT license). This project is independent and not affiliated with DrivenData.
To scaffold a new project from the official template, run `pip install cookiecutter-data-science`
and then `ccds`.

## License

[MIT](LICENSE)
