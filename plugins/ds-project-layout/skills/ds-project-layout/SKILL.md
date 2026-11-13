---
name: ds-project-layout
description: Cookiecutter Data Science (v2) repository layout and code-placement rules for data-science and ML projects. Use before creating a new project, before adding any file or folder, and before moving or reorganizing code. It decides where source code, data, trained models, notebooks, one-off analyses, reports and scripts belong, and what must stay out of git.
---

# Data-science project layout

Use the [Cookiecutter Data Science v2](https://cookiecutter-data-science.drivendata.org/)
layout for every new data-science or ML project. In an existing project, put new
files where this layout says. A project's own documented conventions (README,
CLAUDE.md, AGENTS.md, CONTRIBUTING) take precedence where they differ.

## Target layout

```
├── LICENSE
├── README.md          <- what the project is, how to run it, current results
├── Makefile           <- one-word entry points: make data, make features, make train
├── pyproject.toml     <- package metadata and tool config; the module is installable
├── requirements.txt   <- or a uv/poetry lock file
├── data/              <- gitignored
│   ├── raw/           <- original, immutable inputs; never edited in place
│   ├── external/      <- third-party data
│   ├── interim/       <- intermediate transforms
│   └── processed/     <- final, model-ready tables and feature files
├── models/            <- trained models, predictions, model summaries (gitignored)
├── notebooks/         <- exploration only; named <n.m>-<initials>-<topic>.ipynb
├── references/        <- data dictionaries, papers, manuals
├── reports/           <- generated analysis (HTML, Markdown, CSV)
│   └── figures/
├── docs/              <- longer documentation, if any
└── <module_name>/     <- importable source code
    ├── __init__.py
    ├── config.py      <- paths and constants; the only place paths are defined
    ├── dataset.py     <- download, load and split data
    ├── features.py    <- feature engineering (a features/ package once it grows)
    ├── modeling/
    │   ├── __init__.py
    │   ├── train.py
    │   └── predict.py
    └── plots.py
```

Two optional additions keep research projects tidy without new top-level clutter:

| Folder | Holds |
|---|---|
| `scripts/` | Glue that is not library code: download, remote or cluster job drivers, submission helpers |
| `analysis/<round>/` (or `experiments/<round>/`) | One-off ablations and investigations for a round of work, each round with a short README |

An `EXPERIMENTS.md` at the root records what was tried, the numbers, and what was kept.

## Where does this file go?

| You are adding | Put it in |
|---|---|
| A new feature family | `<module>/features.py`, or `<module>/features/<family>.py` once there are several |
| A new model type (GBDT, neural net, foundation model) | `<module>/modeling/<model_name>/`, with its remote/GPU driver beside it |
| Data loading, splits, cross-validation folds | `<module>/dataset.py` |
| A path, seed, split date or other constant | `<module>/config.py` |
| A one-off investigation | `analysis/<round>/` |
| Exploratory work with plots | `notebooks/` |
| A figure or table for a write-up | `reports/` and `reports/figures/` |
| Raw downloads, caches, feature matrices | `data/` (gitignored) |
| Checkpoints, predictions, run logs | `models/` or another gitignored output folder |

## Rules for any change

1. **Look before you add.** Find where similar code already lives and put the new file
   beside it. Never create a top-level folder for one experiment or model.
2. **Commit code, not artifacts.** Commit code, configs, small JSON/CSV results and docs.
   Keep data, feature files, `.npy/.npz/.parquet/.pt/.ckpt`, archive parts, zips and run logs
   out of git. Check every new artifact path with `git check-ignore`.
3. **Define paths once.** Paths come from `config.py`. Scripts run from the repo root.
   Committed code has no absolute machine paths such as `/Users/<name>/...` or `C:\...`.
4. **Import, don't patch `sys.path`.** Make the module installable (`pip install -e .`) or
   run with `python -m <module>.<sub>`.
5. **Keep entry points thin.** A CLI script parses arguments and calls library functions.
   Logic used in two places moves into the module.
6. **Notebooks explore; the module ships.** Code a notebook reuses moves into the module.
7. **Make results traceable.** Each reported number names the command and commit that
   produced it.
8. **Migrate existing repos gradually.**
   - Map the current folders onto this layout.
   - Move files when asked or when you are already editing them.
   - Never move files a running job depends on.
   - Use `git mv` so history follows.
   - After a move, search code, shell scripts and docs for the old path, fix each match,
     then smoke-test the entry points.
   - Large data folders can stay where they are if `config.py` points at them and the
     README maps them to the layout names.
9. **Keep secrets out of git.** Credentials, tokens and personal details never go in
   tracked files or logs.

## Checklist before finishing a change

- [ ] New files sit in the layout's folders; no new top-level directories.
- [ ] Generated and large files are gitignored.
- [ ] No hard-coded absolute paths and no new `sys.path` edits.
- [ ] README or EXPERIMENTS.md is updated if behaviour or results changed.
