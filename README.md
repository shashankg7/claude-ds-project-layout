# ds-project-skills: Claude Code skills for data science and ML research

A small collection of [Claude Code](https://code.claude.com/docs) skills for people who
build ML models and write papers about them. Each skill lives in its own folder under
[`skills/`](skills/) and can be installed as a plugin or copied as a plain skill.

| Skill | What it does |
|---|---|
| [ds-project-layout](skills/ds-project-layout/SKILL.md) | Keeps data-science and ML repositories in the Cookiecutter Data Science v2 layout. Claude reads it before creating a project, adding a file or moving code. |
| [ml-paper-writing](skills/ml-paper-writing/SKILL.md) | One skill for writing and reviewing research papers: an author style profile and review procedure for IR, recommender-systems and off-policy-evaluation papers, on top of general guidance for NeurIPS, ICML, ICLR, ACL, AAAI and COLM (narrative structure, citation verification, reviewer checklists, LaTeX templates) from [AI-Research-SKILLs](https://github.com/Orchestra-Research/AI-Research-SKILLs). |

## Install

### As plugins (recommended)

```bash
claude plugin marketplace add shashankg7/ds-project-skills
```

```bash
claude plugin install ds-project-layout@ds-project-skills
```

```bash
claude plugin install ml-paper-writing@ds-project-skills
```

Inside a Claude Code session, the one-step equivalents are:

```
/plugin install ds-project-layout --marketplace shashankg7/ds-project-skills
/plugin install ml-paper-writing --marketplace shashankg7/ds-project-skills
```

### As plain skills

Copy the skill folders you want into your personal skills (applies to all projects):

```bash
git clone https://github.com/shashankg7/ds-project-skills
mkdir -p ~/.claude/skills
cp -r ds-project-skills/skills/ds-project-layout ~/.claude/skills/
cp -r ds-project-skills/skills/ml-paper-writing ~/.claude/skills/
```

To apply a skill to one repository and share it with collaborators, copy it to
`.claude/skills/` in that repository instead.

## ds-project-layout

New work lands in predictable places: features in the module, each model family under
`modeling/`, one-off investigations under `analysis/`, and data and checkpoints out of
git. No more `dcn/`, `final_v2/` and `try_this/` folders piling up at the repo root.

- **The target layout:** `data/{raw,external,interim,processed}`, `models/`, `notebooks/`,
  `references/`, `reports/`, and an importable module with `config.py`, `dataset.py`,
  `features.py` and `modeling/`.
- **A "where does this file go?" table** for features, new model types, data loading,
  constants, one-off analyses, figures, checkpoints and logs.
- **Rules for every change:** no new top-level folders, artifacts gitignored, paths
  defined once in `config.py`, no `sys.path` patches, thin entry points, traceable
  results, no secrets in git.
- **Safe migration of existing repos:** move files gradually, never under a running job,
  using `git mv`, fixing every old path and smoke-testing afterwards.
- **A short checklist** Claude runs before finishing a change.

The skill defers to a project's own documented conventions (README, CLAUDE.md, AGENTS.md,
CONTRIBUTING) and is the default where a project has none.

Claude loads a skill when its description matches the task. To have the layout applied to
every change, add this to `~/.claude/CLAUDE.md` (all projects) or to a project's `CLAUDE.md`:

```markdown
## Repository layout
Follow the `ds-project-layout` skill for every new project and every code change.
Read it before creating a project, adding a file or folder, or moving code.
```

## ml-paper-writing

**Author style profile.** The top of [SKILL.md](skills/ml-paper-writing/SKILL.md) and
[references/author-style.md](skills/ml-paper-writing/references/author-style.md) record the
maintainer's own writing style and review procedure for IR, recommender-systems and
off-policy-evaluation papers. This covers how to review a draft (section by section, find →
replace edits labelled Must/Should/Optional, rewrites only on request), an editing contract
that protects math, numbers and citations, venue-specific structure, abstract and
introduction moves, notation, an experiments review checklist, claim calibration and
recurring errors. For papers in that style it overrides the generic recipes. Adapt it to your
own style or ignore it for other papers.

**General guide.** Covers the narrative structure of an ML paper, section-by-section advice, citation
lookup and verification (Semantic Scholar, arXiv, CrossRef), reviewer guidelines,
pre-submission checklists, and LaTeX templates for NeurIPS 2025, ICML 2026, ICLR 2026,
ACL, AAAI 2026 and COLM 2025. For systems venues it points to the upstream
`systems-paper-writing` skill. The citation helpers use the Python packages
`semanticscholar`, `arxiv`, `habanero` and `requests`.

## Credits

- **ds-project-layout** follows [Cookiecutter Data Science](https://github.com/drivendata/cookiecutter-data-science)
  by DrivenData (MIT). This project is independent and not affiliated with DrivenData.
  To scaffold a new project from the official template, run `pip install cookiecutter-data-science`
  and then `ccds`.
- **ml-paper-writing**: the general guide is from [AI-Research-SKILLs](https://github.com/Orchestra-Research/AI-Research-SKILLs)
  by Orchestra Research (MIT, see [its LICENSE](skills/ml-paper-writing/LICENSE)), with
  links to its sibling skills pointed at the upstream repository. The author style profile
  is original to this repository. The conference LaTeX
  templates belong to their respective venues.

## License

[MIT](LICENSE), except where a skill folder carries its own LICENSE.
