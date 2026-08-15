# table-remodeler

Purpose: transforms tabular data files through JSON-configurable operation pipelines; primary use case is neuroimaging event file preprocessing with optional HED (Hierarchical Event Descriptors) annotation support. Not in scope: HED validation itself - that lives in hedtools (hed-python).

The PyPI distribution is `table-remodeler`; the importable package is `remodeler`. Always import from `remodeler`, never `remodel`.

## Commands

Test framework: unittest. Never convert the suite from one style to the other as a side effect of other work.

- Install dev env: `pip install -e .[test,docs,examples]` (editable install required before running tests)
- Run tests: `python -m unittest discover tests -v`
- Single test: `python -m unittest tests.test_dispatcher.Test.test_constructor`
- Lint: `ruff check .`
- Format check: `ruff format --check .` (auto-fix with `ruff format .`)
- Spell check: `typos .`

CI runs all of these on push/PR to `main`: tests on Linux and Windows across supported Python versions, ruff, typos, a Sphinx docs build, and link validation (see `.github/workflows/`).

## Layout

- `remodeler/` - the package. `dispatcher.py` orchestrates operation execution; `backup_manager.py` handles dataset backup/restore; `remodeler_validator.py` validates remodeling JSON; `cli/` has the entry points; `operations/` has all operation classes, registered in `operations/valid_operations.py`.
- `tests/` - unittest suite mirroring `remodeler/`; test data in `tests/data/`.
- `docs/` - Sphinx documentation.
- `pyproject.toml` - build config, all dependencies, ruff and typos settings.
- `.status/` - working notes. Gitignored; local to each machine.

## Conventions that differ from defaults

- **ASCII only** in prose, code, comments, and filenames: `-` not em or en dashes, `->` not arrows, `...` not an ellipsis character, straight quotes. Exception: genuine data (author names, dataset titles, recorded API responses) keeps whatever characters it actually contains.
- Google-format docstrings with `Parameters:` (not `Args:`).
- Ruff config lives in `pyproject.toml`: line length 120, target py310, with `E501` and `N802/803/806` ignored (lowercase naming in scientific code).

## Rules that are easy to get wrong

- Import from `remodeler`, not `remodel` - the distribution name and the package name differ.
- Do not hardcode HED schema versions; use `Dispatcher`'s `hed_versions` parameter. Schemas are auto-cached in the user's `.hedtools/` directory.
- At runtime, summaries save to `remodel/summaries/` inside the dataset - that spelling is part of the on-disk format, not a typo.
- Adding an operation: create `remodeler/operations/<name>_op.py` inheriting `BaseOp` (define `NAME`, `PARAMS`, `do_op`, `validate_input_data`), then register it in `remodeler/operations/valid_operations.py`.

## Related repositories

- `hed-python` - provides the required `hedtools` dependency (HED operations). Not vendored here.
- `hed-schemas` - the HED schema definitions that hedtools fetches.

## Where the thinking lives

`.status/` is gitignored, so it exists only on the machine that wrote it and never in a fresh clone or worktree.

- `.status/README.md` - the index. Read this first; it lists what is active.
- `.status/decisions.md` - why things are the way they are. Read before proposing structural changes. Append entries; never rewrite one.
- `.status/plans/*.md` - active plans. Check the `Status:` header and the `[ ]` / `[x]` markers before starting work.
- `.status/local-environment.md` - this machine's paths, interpreter, and quirks. Tool-agnostic. Never copy its contents into a committed file.
- IMPORTANT: do not read `.status/archive/` unless a file is named for you. Nothing new is created at the `.status/` root.

## Working agreements

- IMPORTANT: every file written to `.status/` opens with a `For humans:` summary - three or four sentences, at the very top: what the file is and what a person needs to take from it. The same applies to a long answer in a session: lead with the conclusion.
- IMPORTANT: temporary scripts, experiments, and one-off test files go in `.status/scratch/` - **never the repository root**. Delete them when the experiment ends; anything in `scratch/` may be deleted unread.
- IMPORTANT: never delete or rewrite a file under `.status/` without asking first. Appending is fine.
- For a change spanning more than three files, write a plan to `.status/plans/` and stop for review before editing.
- When you are guessing about an external API or data format, say so explicitly rather than assuming.
- Show evidence, not assertions: the command you ran and its actual output.
- Do not commit, push, or create branches unless asked.
